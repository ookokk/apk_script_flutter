
terminal generate keygen
```
keytool -genkey -v -keystore D:\key.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias key
```

---

key.properties:

```
storePassword= 
keyPassword= 
keyAlias=key
storeFile=D:/key.jks
```

---

build.gradle içerisine yazılacak olan kodlar:

```
def keyProperties = new Properties()
def keyPropertiesFile = rootProject.file('key.properties')
if(keyPropertiesFile.exists()){
    keyProperties.load(new FileInputStream(keyPropertiesFile))
}
```

```
signingConfigs{
        release{
            keyAlias keyProperties['keyAlias']
            keyPassword keyProperties['keyPassword']
            storeFile file(keyProperties['storeFile'])
            storePassword keyProperties['storePassword']
        }
    }
```

---

APK olusturmak için terminale yazılacak olan komut:

```
flutter build apk --split-per-abi
```
appbundle = 
flutter build appbundle
flutter build appbundle --build-name=1.0.0 --build-number=1
