# CoreDNS-PQC
This is a **fork of CoreDNS** that integrates support for **Post-Quantum Cryptography (PQC)** signature algorithms through a custom plugin called `dnssec_pqc`. It is intended for research and testing purposes within the context of DNSSEC and PQC algorithm evaluation.

[![CoreDNS](https://coredns.io/images/CoreDNS_Colour_Horizontal.png)](https://coredns.io)

## PQC DNSSEC Plugin

The `dnssec_pqc` plugin extends CoreDNS to allow DNSSEC zone signing and validation using a set of post-quantum signature algorithms. It builds upon the original `dnssec` plugin by replacing or augmenting cryptographic operations with post-quantum alternatives.

### Supported Algorithms and Identifiers

The plugin currently supports the following post-quantum signature schemes, identified by custom algorithm IDs:

## Supported Algorithms
| Algorithm        | ID |
|------------------|----|
| FALCON512        | 17 |
| DILITHIUM2       | 18 |
| SPHINCS_SHA2     | 19 |
| MAYO1            | 20 |
| SNOVA            | 21 |
| FALCON1024       | 27 |
| DILITHIUM3       | 28 |
| SPHINCS_SHAKE    | 29 |
| MAYO3            | 30 |
| SNOVASHAKE       | 31 |
| FALCONPADDED512  | 37 |
| DILITHIUM5       | 38 |
| FALCONPADDED1024 | 47 |

## Installation
```bash
git clone https://github.com/Juligent/coredns
cd coredns
go mod tidy
go clean
go build
```

## Configuration example of the Corefile


```bash
example.org:1053 {
    dnssec {
        key file <your_path>/dnssec_test/Kexample.org.+XXX+XXXXX
    }
    forward . 8.8.8.8
    log
}
.:1053 {
    forward . 8.8.8.8
    log
}
```


## Dependencies

This fork depends on a **custom version** of the [`miekg/dns`](https://github.com/miekg/dns) library, modified to support PQC extensions.
  
> https://github.com/qursa-uc3m/dns  
> Branch: `pqcintegrated`

The fork uses this versión, in its `go.mod` file there should be the instance:
```bash
replace github.com/miekg/dns => github.com/qursa-uc3m/dns pqcintegrated
```
to enable PQC support.



## License
Apache License 2.0
