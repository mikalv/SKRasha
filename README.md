# SKRasha
Encrypt your data with RSA+AES in simple Function , It's also has sign function , I will update README.md later.

## Make your RSA keys
1. **Make your private key in Terminal.**  
``openssl genrsa -out rsa_private_key.pem 1024``  
2. **Make your public key**  
``openssl rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem``  
3. **Change your private key into PKCS8**  
``openssl pkcs8 -topk8 -inform PEM -in rsa_private_key.pem -outform PEM -nocrypt -out private_key.pem``  
  
Then we will use **step2** and **step3** created public and private keys

## How to use 
```
    NSString* private_key_string = @"MIICdwIBADANBgkqhkiG9w0BAQEFAASCAmEwggJdAgEAAoGBAK78zUPg8fwoKERo\
    8ll2CDfqAsCbpTmfc29CR+8pSZi6ekFtcx4UOPLWwpnPqiKr+hAOqqPtrulg5KLM\
    HPNgPkxIZRMTD6hyCVTFfc4g0M3rXwuizDeczu8ykQMK+BSYH4bajfJ1ewhlVSx3\
    03y1vtLMoYOpzB2pUoi5MNItfwDvAgMBAAECgYEAmnk0wx1KwWy5z1pNxse5jZKZ\
    B2rfOrUV9DuwwOHTxG2qCyQRoZX8h/MqKxn1eVIUGCS6Yqgp5n/Qlh5V2Es38i0z\
    /4jMPvUtRo9siXk5wv14/tAoECygI94NmaIokNxQh3xAbqpATt0181IAtTRJKLKu\
    kyuNKGgplZsyHZt9CyECQQDep2VCLcMCNwVDrjApMLqS2kTg1b2mZfRz6OE9/ckb\
    aoxbivg0QD8hljp50PRxEyqvq2y1nc0W/yG6gyCUsy2pAkEAyTHdlYA0JCUzFkoG\
    PwwNQq1g2K0wcZTB78afBv8dENIqjmknbio5IQh5+HhBtnXhbPDTHDdcBrynnzdb\
    0R9o1wJARysSfrjJ4Gdd02hWFJRyzoXeBk/Lsuhb3sDNXldEdPL1sj0VYP44L7Ap\
    OM7Fk28g8c3FjbfG2lbqnQdU3rL3IQJBAL0QwRvGWDlHQ9TER05j8uofp4y2Y3m4\
    wu6iBbs7bYLrHNaq9kTOJNVn88aMq6Pc7rPDM3+mfjJOgm5aRUwlag0CQA+TPnax\
    7EHBgQQwC3ccjLJNPLaJRzhivw7tmUJ9Yuzy9wZZp9KcpUrFdEdaNffbECGAE4FQ\
    eDNNLfvHyvWnbc4=";
    
    
    NSString* public_key_string = @"MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCu/M1D4PH8KChEaPJZdgg36gLAm6U5n3NvQkfvKUmYunpBbXMeFDjy1sKZz6oiq/oQDqqj7a7pYOSizBzzYD5MSGUTEw+ocglUxX3OINDN618Losw3nM7vMpEDCvgUmB+G2o3ydXsIZVUsd9N8tb7SzKGDqcwdqVKIuTDSLX8A7wIDAQAB";
    
    
    HBRSAHandler* handler = [HBRSAHandler new];
    
    [handler importKeyWithType:KeyTypePrivate andkeyString:private_key_string];
    [handler importKeyWithType:KeyTypePublic andkeyString:public_key_string];
    _handler = handler;
    
    NSString *orgString = @"name=Stark小伙挺溜&age=18";
    
    //aes
    NSString *aesStr = [orgString aes256_encrypt:@"heheda"];
    NSLog(@"aes\n%@",aesStr);
    
    //rsa
    NSString *rsaStr = [_handler encryptWithPublicKey:aesStr];
    NSLog(@"rsa\n%@",rsaStr);
    
    //dersa
    NSString *deRsaStr = [_handler decryptWithPrivatecKey:rsaStr];
    NSLog(@"deRsa\n%@",deRsaStr);
    
    //deaes
    NSString* deStr = [deRsaStr aes256_decrypt:@"heheda"];
    NSLog(@"deaes\n%@",deStr);
```

## Input to your Project
make sure the search path in Xcode contains openssl 

![Alt text](https://github.com/Stark1937/SKRasha/blob/master/SearchPath.png?raw=true)
## Thanks
this repo is base on [iOSRSAHandler](https://github.com/HustBroventure/iOSRSAHandler "Title").