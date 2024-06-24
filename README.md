# PIB_Agent

1. Install Package
```
conda create -n pib_agent python=3.10
echo "export PIB_AGENT_HOME=/path/to/current/directory" >> ~/.bashrc
source ~/.bashrc
conda activate pib_agent
```

2. Clone this repository and navigate to PIB_Agent folder
```
git clone https://github.com/gray311/PIB_Agent
cd PIB_Agent
```

3. Install Package Related to Python Environment
```
mkdir lib
cd lib

# install android_env
git clone https://github.com/google-deepmind/android_env
cd android_env
pip install -e .
cd ..

# install auto_ui
git clone https://github.com/cooelf/Auto-GUI
cd Auto-GUI
pip install -r requirements.txt
cd ..

cd $PIB_AGENT_HOME

# others
pip install -r requirements.txt 
```

4. Android emulators (Android Studio). If your system is linux, please refer to the [link](https://github.com/b-moca/b-moca), the following applies to macos
```
# step 1: Install ADB
brew ...

# adb --version
# Android Debug Bridge version 1.0.41
# Version 35.0.1-11580240
# Installed as /opt/homebrew/bin/adb
# Running on Darwin 23.4.0 (arm64)

# step 2: Install Java (JDK-17)
# https://www.oracle.com/cn/java/technologies/downloads/#jdk17-mac
# download ARM64 DMG Installer (M-x silicon)

# step 3: Install SDK manager 
# https://developer.android.com/studio?hl=zh-cn#downloads
# download commandlinetools-mac-11076708_latest.zip
export ANDROID_SDK_ROOT=$HOME/.local/share/android/sdk
mkdir -p $ANDROID_SDK_ROOT/cmdline-tools

unzip commandlinetools-mac-11076708_latest.zip -d $ANDROID_SDK_ROOT/cmdline-tools 
mv $ANDROID_SDK_ROOT/cmdline-tools/cmdline-tools $ANDROID_SDK_ROOT/cmdline-tools/latest
echo "export PATH=$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/cmdline-tools/tools/bin" >> ~/.bashrc 
source ~/.bashrc

# Check sdkmanager version
sdkmanager --version
echo "DOWNLOAD ANDROID SDK DONE!"

# Configure sdkmanager
sdkmanager --licenses
sdkmanager --update --verbose

# Install Android Image version 29 
sdkmanager "emulator" 
sdkmanager "platform-tools" 
sdkmanager "platforms;android-29" 
sdkmanager "system-images;android-29;google_apis;arm64-v8a" 

# Check emulator version
echo "export PATH=$PATH:~/.local/share/android/sdk/emulator" >> ~/.bashrc 
source ~/.bashrc
emulator -version 
# Android emulator version 34.2.15.0 (build_id 11906825) (CL:N/A)

# step 4: Install Appium
# Version check
node -v # v22.2.0
npm -v # 10.8.1

# Install appium
npm install -g appium 
npm install wd
npm install -g appium-doctor
appium driver install uiautomator2

# Set environment variable and check appium driver
echo “export export ANDROID_SDK_ROOT=$HOME/.local/share/android/sdk” >> ~/.bashrc 
source ~/.bashrc

appium driver list --installed # uiautomator2 
appium -v # 2.x.x
```

5. APK download. (ToDO)
```
mkdir logs
bash install.sh
```

6. Emulator launch.
```
emulator -port 5554 -avd pixel_3_test_00  -no-audio -no-skin -no-snapshot -gpu "swiftshader_indirect" 
```

7. Run AppAgent. (Please refer to [link](https://github.com/mnotgod96/AppAgent/))
```
python learn.py
```