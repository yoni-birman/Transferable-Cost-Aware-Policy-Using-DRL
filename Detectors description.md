
# The PE detectors

## pefile
This detector uses seven features extracted from the PE header: DebugSize, ImageVersion, IatRVA, ExportSize, ResourceSize, VirtualSize2, and NumberOfSections, all presented in ~\cite{p33}. Using those features, we trained a Decision Tree classifier.

## byte3g
This detector uses features extracted from the raw binaries of the PE file ~\cite{p31}. 
First, it constructs trigrams of bytes. 
Second, it computes the trigrams' term frequencies (TFs).
Third, we calculate the document frequencies (DFs), which represent the ubiquity of a trigram in the entire dataset. 
Finally, since the number of features can be substantial (up to 256^3), we use the top 300 DF-valued features for classification. 
Using the selected features, we trained a Random Forest classifier with 100 trees.

## opcode2g
This detector uses features based on the disassembly of the PE file ~\cite{p34}. 
First, it disassembles the file and extracts the opcode of each instruction.
Second, it generates bigram representations of the opcodes. 
Third, both the TF and DF values are computed for each bigram. 
Finally, we select the 300 bigrams with the highest DF values and use their TF values as features. 
Using the selected features, we trained a Random Forest classifier with 100 trees.

## manalyze
This detector is based on Manalyze (https://github.com/JusticeRage/Manalyze) an open source scanning tool used by security products, such as DFN-CERT (https://www.dfn-cert.de/en.html) and ANY.RUN.(https://any.run)
This detector offers multiple types of static analysis, namely plug-ins, which include: packed executable detection, ClamAV and YARA signatures, detection of suspicious import, detection of cryptographic algorithms, and verification of Authenticode signatures. 
Each plug-in returns one of three values: benign, possibly malicious, and malicious. 
Manalyze does not offer an out-of-the-box method for combining the plugin scores, Thus we trained a Decision Tree classifier with the scores of the plug-ins as features. \newline

# The APK detectors:

## manifest
This detector, suggested by Sato \etal~\cite{sato2013detecting}, classifies APK files by analyzing their AndroidManifest.xml.
A heuristic scoring mechanism selects six features: permission, intent filter {action, category, priority}, process name, and number of redefined permissions.
The textual features were converted to numeric values using a malignancy score computed based on statistical analysis. Then a Decision Tree classifier is trained using these features.

## mmda
Wang \etal~\cite{wang2016mmda} utilized 122 features from AndroidManifest.xml file: 40 most frequent permissions, 40 most frequent hardware features, 40 most frequent actions, and two additional features --- number of permissions and number of receiver actions. A Random Forest classifier with 100 trees was trained using these features.


## bytecode
This detector performs frequency analysis of the Dalvik bytecode instructions ~\cite{kang2013android}. 
Android apps are developed in Java, compiled to Dalvik bytecode, and executed in either Dalvik or Android Runtime virtual machines. This detector that analyzes the app's behaviour evaluates the frequencies of the 218 bytecode instructions and uses them as features. 
A Random Forest classifier with 100 trees was trained to classify the file.

## dalvikapi
This detector uses permissions and Dalvik API calls to classify APKs ~\cite{chan2014static}. 
The permissions are extracted from the Android manifest file, while the API calls are extracted using the following process:
First, the file inside the APK is converted to a Java Archive (JAR) file. 
Second, all class files are extracted from the decompressed JAR. 
Third, the class files are decompiled into Java files that contain all API calls.
Information Gain (IG) is then applied to select the most useful permissions and API calls, keeping only those whose IG values are positive.
Finally, training a Random Forest model with 500 trees to classify the file. 

# Discussion: detector efficacy and relative performance.
It is important to note that while we made sure our chosen detectors are both effective (as shown in Section  IV-B) and commonly used in recent academic literature ~\cite{ucci2019survey}, we did not attempt to implement current top-performing detectors in our experiments. 
We made this decision because a focus on such detectors is immaterial to the main contribution of this study. Our goal is to show that a group of detectors with different performance levels and complementary strengths can be used cost-effectively. 
The top-performing detectors of today cannot individually cope with all of today's attacks and are likely to be less effective in the future, and their reduced effectiveness will require an intelligent approach to combine their input in a cost-effective manner to compensate for their deteriorating performance. 
In fact, our results in Section V-F, where we evaluate SPIREL's to re-calibrate itself after one detector stops working directly address this point. 
The main contribution of SPIREL is the ability to cost-effectively leverage existing detection capabilities, not necessarily employing the single most accurate detectors.

