**Current version support for Java 8 only, if you get problem with UnsupportedClassVersionError: hashkey/Design : Unsupported major.minor version 52.0. Do please update your java to version 8**

    * If you can not open HashKeyHelper.jar, please open terminal then: chmod +x HashKeyHelper.jar *

When you build an Java application project that has a main class, the IDE
automatically copies all of the JAR
files on the projects classpath to your projects dist/lib folder. The IDE
also adds each of the JAR files to the Class-Path element in the application
JAR files manifest file (MANIFEST.MF).

To run the project from the command line, go to the dist folder and
type the following:

java -jar "HashKey.jar" 

To distribute this project, zip up the dist folder (including the lib folder)
and distribute the ZIP file.

Notes:

* If two JAR files on the project classpath have the same name, only the first
JAR file is copied to the lib folder.
* Only JAR files are copied to the lib folder.
If the classpath contains other types of files or folders, these files (folders)
are not copied.
* If a library on the projects classpath also has a Class-Path element
specified in the manifest,the content of the Class-Path element has to be on
the projects runtime path.
* To set a main class in a standard Java project, right-click the project node
in the Projects window and choose Properties. Then click Run and enter the
class name in the Main Class field. Alternatively, you can manually type the
class name in the manifest Main-Class element.

## I. Introduction

With many applications which were written in Java language such as Android 
applications, Java desktop applications and all JAR libraries will be decoded 
and your achievement will be lost.

Even your secret key which connect to your Facebook account, Google email will
be lost too.

Due to that I write this tool is protect your secrete key or any private
information data in your application.

Moreover, this tool provide a function to generate hashkey which is used to 
sign your application with Facebook (https://developers.facebook.com/)

## II. How to use

### 1. UI guide

This tool is written in java language, however it using proguard technology to 
obfuscate source code.

Let me show you how to use it:

- KeyStore path: it's path of your keystore, file used to signed your apk 
android 

- keytool path: it's in your java home. 
```
Mac: /Library/Java/VirtualMachine/{YOUR_CURRENT_VERSION}/Content/Home/bin

Windows: C:/Windows/Programs/Java/{YOUR_CURRENT_VERSION}/bin

Linux: with the same to Java home path ( i do not remember the path, because 
```
with all linux we can using and configure java path any where)

- Key password: It's your keystore password

- Alias: ignore it, because it's will be filled when you generate hashkey

- Encode resource: Your data which need to be protect, please add all private
information in 1 properties file, then tool will be encode your file content
with AES algorithm

- Generate button: when you select it, tool will works and generate a hashkey
for you

- Copy button: copy hashkey above to your clipboard then you can paste it
anywhere.

- Encode button: encode your data in properties file above.

###2. Functions

- This tool will be saved last input information (keystore path, password in 
history.properties..., of course, they are encoded)

- This tool will be work multi-platforms (I hope so): Mac, Windows, Linux

###3. Implement

When you encoded your data, please copy encoded.properties (change the name if
you want), and all in lib folders to your project (gradle, eclipse...)

To get your data, please use Aes.decryptFromBase64(data, signature_in_your 
keystore)

you can get your hashkey of your keystore (used to signed your apk, if debug 
mode, will be debug.keystore) with the flowing android's code:
```
    public static String getHashKey() {
        Context mAppContext = GlobalApplication.getInstance();
        try {
            PackageInfo info = mAppContext.getPackageManager()
                    .getPackageInfo(mAppContext.getPackageName(), PackageManager.GET_SIGNATURES);
            String sig = null;
            Signature signature = info.signatures[0];
            MessageDigest md = MessageDigest.getInstance("SHA");
            md.update(signature.toByteArray());
            sig = Base64.encodeToString(md.digest(), Base64.DEFAULT);
            //Toast.makeText(context, sig, Toast.LENGTH_LONG).show();
            return sig;
        } catch (PackageManager.NameNotFoundException e) {
            //e.printStackTrace();
        } catch (NoSuchAlgorithmException e) {
            //e.printStackTrace();
        }
        return null;
    }
```

Or using the hashkey created by this tool. (I recommend to use code above)

##III. Conclusion

This tool provide you an extra way to project your application. 

If you have any question, don't be shy, email me to nguyen.viet.manh@framgia.com
I will answer you asap.

Thank you for your attention.

