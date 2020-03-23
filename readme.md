Create blazing fast self signed ssl certificates without OpenSSL using BlazeCert™

## Install
```
npm install -g blazecert
```

## CLI

### Create a Certificate Authority
```
$ blazecert create-ca --help

  Usage: create-ca [options]

  Options:
    --organization [value]  Organization name (default: "Test CA")
    --country-code [value]  Country code (default: "US")
    --state [value]         State name (default: "California")
    --locality [value]      Locality address (default: "San Francisco")
    --validity [days]       Validity in days (default: 365)
    --key [file]            Output key (default: "ca.key")
    --cert [file]           Output certificate (default: "ca.crt")
    -h, --help              output usage information
```

### Create a Certificate

```
$ blazecert create-cert --help

  Usage: create-cert [options]

  Options:
    --ca-key [file]     CA private key (default: "ca.key")
    --ca-cert [file]    CA certificate (default: "ca.crt")
    --validity [days]   Validity in days (default: 365)
    --key [file]        Output key (default: "cert.key")
    --cert [file]       Output certificate (default: "cert.crt")
    --domains [values]  Comma separated list of domains/ip addresses (default: "localhost,127.0.0.1")
    -h, --help          output usage information
```

## API

### Create a Certificate Authority
```js
import * as blazecert from 'blazecert';

//Create a Certificate Authority
blazecert.createCA({
  organization: 'Hello CA',
  countryCode: 'IND',
  state: 'West Bengal',
  locality: 'Kolkata',
  validityDays: 365
})
.then((ca)=> {
  console.log(ca.key, ca.cert);
})
.catch(err=> console.error(err));
```

### Create a Certificate
```js
import * as blazecert from 'blazecert';
//Create a CA first

//Then create the certificate
blazecert.createCert({
  domains: ['127.0.0.1', 'localhost'],
  validityDays: 365,
  caKey: ca.key,
  caCert: ca.cert
})
.then((cert)=> {
  console.log(cert.key, cert.cert);

  //Create a full chain certificate by merging CA and domain certificates
  console.log(`${cert.cert}\n${ca.cert}`);
})
.catch(err=> console.error(err));
```
