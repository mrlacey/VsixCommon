# VsixCommon

This repository includes functionality used by other Visual Studio extensions. It should be cloned to the same root directory as other repositories that need this functionality.

## signvsix.targets

This is a targets file that handles the automatic signing of Release builds.

Refefernce this file by adding the following (adjust path as necessary) to the end of the csproj file of the extension you wish to sign.

```xml
  <Import Project="..\..\..\VsixCommon\signvsix.targets"/>
```

To use this correctly, you will need to add a reference to the [Microsoft.VSSDK.Vsixsigntool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool) nuget package.

The targets file is dependent upon three values that it expects to find as environment variables.

- **SIGN_CERTIFICATE** - this is the absolute path to the .pfx file.
- **SIGN_PASSWORD** - this is the password for the certificate file.
- **SIGN_CERT_HASH** - this is the SHA1 hash for the certificate.

You can get the SHA1 has by running `certutil -p ********* -dump .\filename.pfx`
The value you want will be listed as the "Cert Hash(sha1)". Make sure you get the one for your certificate, not one higher in the chain.

## ColorHelper

Helper to turn string of color name into a `SolidColorbrush`. Works with names and #RRGGBB values. 
