# Android Permission Analyzer

A static analysis tool to detect over-requesting Android applications. It parses APK manifests to extract declared permissions and uses Androguard to check the DEX bytecode for corresponding API usage.

## The Heuristic
If an app declares a dangerous permission (e.g., `READ_SMS`, `CAMERA`) but the compiled code does not reference the expected API class (e.g., `SmsManager`, `Camera`), it is flagged as a potential over-request. 

*(Note: This is a limited static heuristic. It does not account for reflection or native code, and is intended for educational purposes.)*

## Dataset
Tested on open-source APKs from F-Droid (F-Droid client, Termux, Wikipedia). 

## Results
Testing on these open-source applications yielded no over-requests, confirming that legitimate, well-maintained apps properly align their declared permissions with API usage. The heuristic is designed to catch malicious or poorly developed apps that hide their API usage or request permissions unnecessarily.

## How to Run
1. Install: `pip install androguard`
2. Run the Python script on any folder containing `.apk` files.
