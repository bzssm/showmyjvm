# Security Assessment Report

**Generated:** 2026-06-17T07:32:02.0000000Z

## Summary

| Metric | Count |
|--------|-------|
| Total Findings | 50 |
| CVE Vulnerabilities | 44 |
| CWE Vulnerabilities | 6 |
| Total Rules Assessed | 59 |
| Rules Passed | 53 |

### By Severity

| Severity | Count |
|----------|-------|
| mandatory | 44 |
| optional | 2 |
| potential | 4 |

## CVE Findings (Dependency Vulnerabilities)

### CVE-2026-43512: Apache Tomcat - Digest authenticator will authenticate any unknown user
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-43512](https://github.com/advisories/GHSA-h6fc-48rj-7qqh): Apache Tomcat - Digest authenticator will authenticate any unknown user

Severity: CRITICAL

Affected packages:
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat-catalina` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)

Files: pom.xml

### CVE-2026-43515: Apache Tomcat - Security constraints not correctly applied
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-43515](https://github.com/advisories/GHSA-5m62-pw8w-7w9f): Apache Tomcat - Security constraints not correctly applied

Severity: CRITICAL

Affected packages:
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat-catalina` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)

Files: pom.xml

### CVE-2026-41293: Apache Tomcat - HTTP/2 request headers not validated
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41293](https://github.com/advisories/GHSA-r29c-68gh-xp6x): Apache Tomcat - HTTP/2 request headers not validated

Severity: CRITICAL

Affected packages:
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat-catalina` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)

Files: pom.xml

### CVE-2026-40976: Spring Boot's default security filter chain has no authorization rule with Actuator but without Health
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-40976](https://github.com/advisories/GHSA-8v8j-3hxp-93wr): Spring Boot's default security filter chain has no authorization rule with Actuator but without Health

Severity: CRITICAL

Affected packages:
  - `org.springframework.boot:spring-boot` affected range: `>= 4.0.0, < 4.0.6` (fix: upgrade to 4.0.6)

Files: pom.xml

### CVE-2025-52999: jackson-core can throw a StackoverflowError when processing deeply nested data
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-52999](https://github.com/advisories/GHSA-h46c-h94j-95f3): jackson-core can throw a StackoverflowError when processing deeply nested data

Severity: HIGH

Affected packages:
  - `com.fasterxml.jackson.core:jackson-core` affected range: `< 2.15.0` (fix: upgrade to 2.15.0)

Files: pom.xml

### CVE-2021-46877: jackson-databind possible Denial of Service if using JDK serialization to serialize JsonNode
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** javalin/pom.xml:40, sparkjava/pom.xml:44

[CVE-2021-46877](https://github.com/advisories/GHSA-3x8x-79m2-3w2w): jackson-databind possible Denial of Service if using JDK serialization to serialize JsonNode

Severity: HIGH

Affected packages:
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.10.0, < 2.12.6` (fix: upgrade to 2.12.6)
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.13.0, < 2.13.1` (fix: upgrade to 2.13.1)

Files: javalin/pom.xml:40, sparkjava/pom.xml:44

### CVE-2022-42003: Uncontrolled Resource Consumption in Jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** javalin/pom.xml:40, sparkjava/pom.xml:44

[CVE-2022-42003](https://github.com/advisories/GHSA-jjjh-jjxp-wpff): Uncontrolled Resource Consumption in Jackson-databind

Severity: HIGH

Affected packages:
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.4.0-rc1, < 2.12.7.1` (fix: upgrade to 2.12.7.1)
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.13.0, < 2.13.4.2` (fix: upgrade to 2.13.4.2)

Files: javalin/pom.xml:40, sparkjava/pom.xml:44

### CVE-2022-42004: Uncontrolled Resource Consumption in FasterXML jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** javalin/pom.xml:40, sparkjava/pom.xml:44

[CVE-2022-42004](https://github.com/advisories/GHSA-rgv9-q543-rqg4): Uncontrolled Resource Consumption in FasterXML jackson-databind

Severity: HIGH

Affected packages:
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.13.0, < 2.13.4` (fix: upgrade to 2.13.4)
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.4.0-rc1, < 2.12.7.1` (fix: upgrade to 2.12.7.1)

Files: javalin/pom.xml:40, sparkjava/pom.xml:44

### CVE-2020-36518: Deeply nested json in jackson-databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** javalin/pom.xml:40, sparkjava/pom.xml:44

[CVE-2020-36518](https://github.com/advisories/GHSA-57j2-w4cx-62h2): Deeply nested json in jackson-databind

Severity: HIGH

Affected packages:
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.13.0, <= 2.13.2.0` (fix: upgrade to 2.13.2.1)
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `<= 2.12.6.0` (fix: upgrade to 2.12.6.1)

Files: javalin/pom.xml:40, sparkjava/pom.xml:44

### CVE-2020-25649: XML External Entity (XXE) Injection in Jackson Databind
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** javalin/pom.xml:40, sparkjava/pom.xml:44

[CVE-2020-25649](https://github.com/advisories/GHSA-288c-cq4h-88gq): XML External Entity (XXE) Injection in Jackson Databind

Severity: HIGH

Affected packages:
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.7.0.0, <= 2.9.10.6` (fix: upgrade to 2.9.10.7)
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.10.0.0, <= 2.10.5.0` (fix: upgrade to 2.10.5.1)
  - `com.fasterxml.jackson.core:jackson-databind` affected range: `>= 2.6.0, <= 2.6.7.3` (fix: upgrade to 2.6.7.4)

Files: javalin/pom.xml:40, sparkjava/pom.xml:44

### CVE-2026-44241: Micronaut has unbounded `formattersCache` in `TimeConverterRegistrar` that Allows Memory Exhaustion via `Accept-Language` Header
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-44241](https://github.com/advisories/GHSA-8hjv-92q9-g4xj): Micronaut has unbounded `formattersCache` in `TimeConverterRegistrar` that Allows Memory Exhaustion via `Accept-Language` Header

Severity: HIGH

Affected packages:
  - `io.micronaut:micronaut-context` affected range: `>= 4.3.0, < 4.10.22` (fix: upgrade to 4.10.22)

Files: pom.xml

### CVE-2026-33012: Micronaut Framework vulnerable to a Denial of Service in HTML error response caching
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-33012](https://github.com/advisories/GHSA-2hcp-gjrf-7fhc): Micronaut Framework vulnerable to a Denial of Service in HTML error response caching

Severity: HIGH

Affected packages:
  - `io.micronaut:micronaut-http-server` affected range: `>= 4.7.0, < 4.10.17` (fix: upgrade to 4.10.17)

Files: pom.xml

### CVE-2026-33013: Micronaut vulnerable to DoS via crafted form-urlencoded body binding with descending array indices
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-33013](https://github.com/advisories/GHSA-43w5-mmxv-cpvh): Micronaut vulnerable to DoS via crafted form-urlencoded body binding with descending array indices

Severity: HIGH

Affected packages:
  - `io.micronaut:micronaut-json-core` affected range: `>= 4.0.0-M1, < 4.10.16` (fix: upgrade to 4.10.16)
  - `io.micronaut:micronaut-json-core` affected range: `>= 3.9.0, < 3.10.5` (fix: upgrade to 3.10.5)
  - `io.micronaut:micronaut-json-core` affected range: `< 3.8.13` (fix: upgrade to 3.8.13)

Files: pom.xml

### CVE-2026-50010: Netty: Wrapping plain trust manager silently disables hostname verification
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-50010](https://github.com/advisories/GHSA-c653-97m9-rcg9): Netty: Wrapping plain trust manager silently disables hostname verification

Severity: HIGH

Affected packages:
  - `io.netty:netty-handler` affected range: `>= 4.2.0.Final, < 4.2.15.Final` (fix: upgrade to 4.2.15.Final)
  - `io.netty:netty-handler` affected range: `<= 4.1.134.Final` (fix: upgrade to 4.1.135.Final)

Files: pom.xml

### CVE-2026-48059: Netty HAProxy: Unbalanced Reference Count in Nested PP2_TYPE_SSL TLV Parsing Leads to Memory Exhaustion
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-48059](https://github.com/advisories/GHSA-h2qv-fj59-j46j): Netty HAProxy: Unbalanced Reference Count in Nested PP2_TYPE_SSL TLV Parsing Leads to Memory Exhaustion

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-haproxy` affected range: `>= 4.2.0.Final, <= 4.2.14.Final` (fix: upgrade to 4.2.15.Final)
  - `io.netty:netty-codec-haproxy` affected range: `<= 4.1.134.Final` (fix: upgrade to 4.1.135.Final)

Files: pom.xml

### CVE-2026-47691: Netty has Insufficient Bailiwick Validation for NS Records
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-47691](https://github.com/advisories/GHSA-5pvg-856g-cp85): Netty has Insufficient Bailiwick Validation for NS Records

Severity: HIGH

Affected packages:
  - `io.netty:netty-resolver-dns` affected range: `>= 4.2.0.Final, <= 4.2.14.Final` (fix: upgrade to 4.2.15.Final)
  - `io.netty:netty-resolver-dns` affected range: `<= 4.1.134.Final` (fix: upgrade to 4.1.135.Final)

Files: pom.xml

### CVE-2026-45674: Netty Vulnerable to DNS Cache Poisoning via Missing Bailiwick Checks in CNAME Records
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-45674](https://github.com/advisories/GHSA-676x-f7gg-47vc): Netty Vulnerable to DNS Cache Poisoning via Missing Bailiwick Checks in CNAME Records

Severity: HIGH

Affected packages:
  - `io.netty:netty-resolver-dns` affected range: `>= 4.2.0.Final, <= 4.2.14.Final` (fix: upgrade to 4.2.15.Final)
  - `io.netty:netty-resolver-dns` affected range: `<= 4.1.134.Final` (fix: upgrade to 4.1.135.Final)

Files: pom.xml

### CVE-2026-45416: Netty: SNI handler pre-allocates up to 16 MiB from nine attacker bytes
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-45416](https://github.com/advisories/GHSA-x4gw-5cx5-pgmh): Netty: SNI handler pre-allocates up to 16 MiB from nine attacker bytes

Severity: HIGH

Affected packages:
  - `io.netty:netty-handler` affected range: `>= 4.2.0.Final, <= 4.2.14.Final` (fix: upgrade to 4.2.15.Final)
  - `io.netty:netty-handler` affected range: `<= 4.1.134.Final` (fix: upgrade to 4.1.135.Final)

Files: pom.xml

### CVE-2026-44893: Netty: HAProxy SSL TLV parsing leaks retained slice on invalid TLV length
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-44893](https://github.com/advisories/GHSA-cc37-9q2j-3hfv): Netty: HAProxy SSL TLV parsing leaks retained slice on invalid TLV length

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-haproxy` affected range: `>= 4.2.0.Final, <= 4.2.14.Final` (fix: upgrade to 4.2.15.Final)
  - `io.netty:netty-codec-haproxy` affected range: `<= 4.1.134.Final` (fix: upgrade to 4.1.135.Final)

Files: pom.xml

### CVE-2026-44249: Netty has an IPv6 Subnet Filter Bypass via Incorrect Comparator Masking
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-44249](https://github.com/advisories/GHSA-3qp7-7mw8-wx86): Netty has an IPv6 Subnet Filter Bypass via Incorrect Comparator Masking

Severity: HIGH

Affected packages:
  - `io.netty:netty-handler` affected range: `>= 4.2.0.Final, <= 4.2.14.Final` (fix: upgrade to 4.2.15.Final)
  - `io.netty:netty-handler` affected range: `<= 4.1.134.Final` (fix: upgrade to 4.1.135.Final)

Files: pom.xml

### CVE-2026-42587: Netty: HttpContentDecompressor maxAllocation bypass when Content-Encoding set to br/zstd/snappy leads to decompression bomb DoS
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-42587](https://github.com/advisories/GHSA-f6hv-jmp6-3vwv): Netty: HttpContentDecompressor maxAllocation bypass when Content-Encoding set to br/zstd/snappy leads to decompression bomb DoS

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-http` affected range: `>= 4.2.0.Alpha1, <= 4.2.12.Final` (fix: upgrade to 4.2.13.Final)
  - `io.netty:netty-codec-http2` affected range: `>= 4.2.0.Alpha1, <= 4.2.12.Final` (fix: upgrade to 4.2.13.Final)
  - `io.netty:netty-codec-http` affected range: `<= 4.1.132.Final` (fix: upgrade to 4.1.133.Final)
  - `io.netty:netty-codec-http2` affected range: `<= 4.1.132.Final` (fix: upgrade to 4.1.133.Final)

Files: pom.xml

### CVE-2026-42584: Netty has HttpClientCodec response desynchronization
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-42584](https://github.com/advisories/GHSA-57rv-r2g8-2cj3): Netty has HttpClientCodec response desynchronization

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-http` affected range: `>= 4.2.0.Alpha1, <= 4.2.12.Final` (fix: upgrade to 4.2.13.Final)
  - `io.netty:netty-codec-http` affected range: `<= 4.1.132.Final` (fix: upgrade to 4.1.133.Final)

Files: pom.xml

### CVE-2026-42583: Netty Lz4FrameDecoder is vulnerable to resource exhaustion 
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-42583](https://github.com/advisories/GHSA-mj4r-2hfc-f8p6): Netty Lz4FrameDecoder is vulnerable to resource exhaustion 

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-compression` affected range: `<= 4.2.12.Final` (fix: upgrade to 4.2.13.Final)
  - `io.netty:netty-codec` affected range: `<= 4.1.132.Final` (fix: upgrade to 4.1.133.Final)

Files: pom.xml

### CVE-2026-42579: Netty has a DNS Codec Input Validation Bypass (Encoder + Decoder)
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-42579](https://github.com/advisories/GHSA-cm33-6792-r9fm): Netty has a DNS Codec Input Validation Bypass (Encoder + Decoder)

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-dns` affected range: `>= 4.2.0.Alpha1, <= 4.2.12.Final` (fix: upgrade to 4.2.13.Final)
  - `io.netty:netty-codec-dns` affected range: `<= 4.1.132.Final` (fix: upgrade to 4.1.133.Final)

Files: pom.xml

### CVE-2026-33871: Netty HTTP/2 CONTINUATION Frame Flood DoS via Zero-Byte Frame Bypass
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-33871](https://github.com/advisories/GHSA-w9fj-cfpg-grvv): Netty HTTP/2 CONTINUATION Frame Flood DoS via Zero-Byte Frame Bypass

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-http2` affected range: `< 4.1.132.Final` (fix: upgrade to 4.1.132.Final)
  - `io.netty:netty-codec-http2` affected range: `>= 4.2.0.Alpha1, < 4.2.10.Final` (fix: upgrade to 4.2.11.Final)

Files: pom.xml

### CVE-2026-33870: Netty: HTTP Request Smuggling via Chunked Extension Quoted-String Parsing
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-33870](https://github.com/advisories/GHSA-pwqr-wmgm-9rr8): Netty: HTTP Request Smuggling via Chunked Extension Quoted-String Parsing

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-http` affected range: `< 4.1.132.Final` (fix: upgrade to 4.1.132.Final)
  - `io.netty:netty-codec-http` affected range: `>= 4.2.0.Alpha1, < 4.2.10.Final` (fix: upgrade to 4.2.10.Final)

Files: pom.xml

### CVE-2025-55163: Netty affected by MadeYouReset HTTP/2 DDoS vulnerability
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2025-55163](https://github.com/advisories/GHSA-prj3-ccx8-p6x4): Netty affected by MadeYouReset HTTP/2 DDoS vulnerability

Severity: HIGH

Affected packages:
  - `io.netty:netty-codec-http2` affected range: `>= 4.2.0.Alpha1, <= 4.2.3.Final` (fix: upgrade to 4.2.4.Final)
  - `io.netty:netty-codec-http2` affected range: `<= 4.1.123.Final` (fix: upgrade to 4.1.124.Final)
  - `io.grpc:grpc-netty-shaded` affected range: `< 1.75.0` (fix: upgrade to 1.75.0)

Files: pom.xml

### CVE-2026-39852: Quarkus has Authentication/Authorization bypasses
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-39852](https://github.com/advisories/GHSA-rc95-pcm8-65v9): Quarkus has Authentication/Authorization bypasses

Severity: HIGH

Affected packages:
  - `io.quarkus:quarkus-vertx-http` affected range: `< 3.20.6.1` (fix: upgrade to 3.20.6.1)
  - `io.quarkus:quarkus-vertx-http` affected range: `>= 3.21.0, < 3.27.3.1` (fix: upgrade to 3.27.3.1)
  - `io.quarkus:quarkus-vertx-http` affected range: `>= 3.30.0, < 3.33.1.1` (fix: upgrade to 3.33.1.1)
  - `io.quarkus:quarkus-vertx-http` affected range: `>= 3.34.0, < 3.35.1.1` (fix: upgrade to 3.35.1.1)

Files: pom.xml

### CVE-2026-41284: Apache Tomcat: Unbounded read in WebDAV LOCK and  PROPFIND handling
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-41284](https://github.com/advisories/GHSA-gx5v-xp9w-j4cg): Apache Tomcat: Unbounded read in WebDAV LOCK and  PROPFIND handling

Severity: HIGH

Affected packages:
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat-catalina` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)

Files: pom.xml

### CVE-2026-43513: Apache Tomcat: LockOutRealm treats user names as case-sensitive
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-43513](https://github.com/advisories/GHSA-5mp6-jrq3-r938): Apache Tomcat: LockOutRealm treats user names as case-sensitive

Severity: HIGH

Affected packages:
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat-catalina` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)

Files: pom.xml

### CVE-2026-42498: Apache Tomcat - WebSocket authentication header exposure
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-42498](https://github.com/advisories/GHSA-fv25-8xcx-gqjc): Apache Tomcat - WebSocket authentication header exposure

Severity: HIGH

Affected packages:
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)
  - `org.apache.tomcat:tomcat-catalina` affected range: `< 9.0.118` (fix: upgrade to 9.0.118)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.55` (fix: upgrade to 10.1.55)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.22` (fix: upgrade to 11.0.22)

Files: pom.xml

### CVE-2026-34483: Apache Tomcat has an Improper Encoding or Escaping of Output vulnerability in the JsonAccessLogValve
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-34483](https://github.com/advisories/GHSA-rv64-5gf8-9qq8): Apache Tomcat has an Improper Encoding or Escaping of Output vulnerability in the JsonAccessLogValve

Severity: HIGH

Affected packages:
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 9.0.40, < 9.0.116` (fix: upgrade to 9.0.116)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.54` (fix: upgrade to 10.1.54)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.21` (fix: upgrade to 11.0.21)
  - `org.apache.tomcat:tomcat` affected range: `>= 9.0.40, < 9.0.116` (fix: upgrade to 9.0.116)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.54` (fix: upgrade to 10.1.54)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.21` (fix: upgrade to 11.0.21)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 9.0.40, < 9.0.116` (fix: upgrade to 9.0.116)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.54` (fix: upgrade to 10.1.54)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.21` (fix: upgrade to 11.0.21)

Files: pom.xml

### CVE-2026-34487: Apache Tomcat vulnerable to Insertion of Sensitive Information into Log File
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-34487](https://github.com/advisories/GHSA-x4m4-345f-5h5g): Apache Tomcat vulnerable to Insertion of Sensitive Information into Log File

Severity: HIGH

Affected packages:
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 9.0.13, < 9.0.117` (fix: upgrade to 9.0.117)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 10.1.0-M1, < 10.1.54` (fix: upgrade to 10.1.54)
  - `org.apache.tomcat:tomcat-catalina` affected range: `>= 11.0.0-M1, < 11.0.21` (fix: upgrade to 11.0.21)
  - `org.apache.tomcat:tomcat` affected range: `>= 9.0.13, < 9.0.117` (fix: upgrade to 9.0.117)
  - `org.apache.tomcat:tomcat` affected range: `>= 10.1.0-M1, < 10.1.54` (fix: upgrade to 10.1.54)
  - `org.apache.tomcat:tomcat` affected range: `>= 11.0.0-M1, < 11.0.21` (fix: upgrade to 11.0.21)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 9.0.13, < 9.0.117` (fix: upgrade to 9.0.117)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.54` (fix: upgrade to 10.1.54)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.21` (fix: upgrade to 11.0.21)

Files: pom.xml

### CVE-2026-24880: Apache Tomcat has an HTTP Request/Response Smuggling vulnerability
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-24880](https://github.com/advisories/GHSA-563x-q5rq-57qp): Apache Tomcat has an HTTP Request/Response Smuggling vulnerability

Severity: HIGH

Affected packages:
  - `org.apache.tomcat:tomcat-coyote` affected range: `>= 7.0.0, < 9.0.116` (fix: upgrade to 9.0.116)
  - `org.apache.tomcat:tomcat-coyote` affected range: `>= 10.1.0-M1, < 10.1.52` (fix: upgrade to 10.1.52)
  - `org.apache.tomcat:tomcat-coyote` affected range: `>= 11.0.0-M1, <= 11.0.18` (fix: upgrade to 11.0.20)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 7.0.0, < 9.0.116` (fix: upgrade to 9.0.116)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M1, < 10.1.52` (fix: upgrade to 10.1.52)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, <= 11.0.18` (fix: upgrade to 11.0.20)

Files: pom.xml

### CVE-2026-24734: Apache Tomcat has an Improper Input Validation vulnerability
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-24734](https://github.com/advisories/GHSA-mgp5-rv84-w37q): Apache Tomcat has an Improper Input Validation vulnerability

Severity: HIGH

Affected packages:
  - `org.apache.tomcat:tomcat-coyote` affected range: `>= 11.0.0-M1, < 11.0.18` (fix: upgrade to 11.0.18)
  - `org.apache.tomcat:tomcat-coyote` affected range: `>= 10.1.0-M7, < 10.1.52` (fix: upgrade to 10.1.52)
  - `org.apache.tomcat:tomcat-coyote` affected range: `>= 9.0.83, < 9.0.115` (fix: upgrade to 9.0.115)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 11.0.0-M1, < 11.0.18` (fix: upgrade to 11.0.18)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 10.1.0-M7, < 10.1.52` (fix: upgrade to 10.1.52)
  - `org.apache.tomcat.embed:tomcat-embed-core` affected range: `>= 9.0.83, < 9.0.115` (fix: upgrade to 9.0.115)

Files: pom.xml

### CVE-2026-2332: Jetty has HTTP Request Smuggling via Chunked Extension Quoted-String Parsing
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-2332](https://github.com/advisories/GHSA-355h-qmc2-wpwf): Jetty has HTTP Request Smuggling via Chunked Extension Quoted-String Parsing

Severity: HIGH

Affected packages:
  - `org.eclipse.jetty:jetty-http` affected range: `>= 12.1.0, <= 12.1.6` (fix: upgrade to 12.1.7)
  - `org.eclipse.jetty:jetty-http` affected range: `>= 12.0.0, <= 12.0.32` (fix: upgrade to 12.0.33)
  - `org.eclipse.jetty:jetty-http` affected range: `>= 11.0.0, <= 11.0.27` (no patch available)
  - `org.eclipse.jetty:jetty-http` affected range: `>= 10.0.0, <= 10.0.27` (no patch available)
  - `org.eclipse.jetty:jetty-http` affected range: `>= 9.4.0, <= 9.4.59` (no patch available)

Files: pom.xml

### CVE-2024-13009: **UNSUPPORTED WHEN ASSIGNED** GzipHandler causes part of request body to be seen as request body of a separate request
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2024-13009](https://github.com/advisories/GHSA-q4rv-gq96-w7c5): **UNSUPPORTED WHEN ASSIGNED** GzipHandler causes part of request body to be seen as request body of a separate request

Severity: HIGH

Affected packages:
  - `org.eclipse.jetty:jetty-server` affected range: `>= 9.4.0, <= 9.4.56` (fix: upgrade to 9.4.57.v20241219)

Files: pom.xml

### CVE-2026-40973: Spring Boot accepts predictable temp directory without ownership verification
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-40973](https://github.com/advisories/GHSA-wwpq-f5c3-7hvx): Spring Boot accepts predictable temp directory without ownership verification

Severity: HIGH

Affected packages:
  - `org.springframework.boot:spring-boot` affected range: `>= 4.0.0, < 4.0.6` (fix: upgrade to 4.0.6)
  - `org.springframework.boot:spring-boot` affected range: `>= 3.5.0, < 3.5.14` (fix: upgrade to 3.5.14)
  - `org.springframework.boot:spring-boot` affected range: `>= 3.4.0, <= 3.4.15` (no patch available)
  - `org.springframework.boot:spring-boot` affected range: `>= 3.3.0, <= 3.3.18` (no patch available)
  - `org.springframework.boot:spring-boot` affected range: `<= 2.7.32` (no patch available)

Files: pom.xml

### CVE-2026-22733: Spring Boot has an Authentication Bypass under Actuator CloudFoundry endpoints
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** spring-boot/pom.xml:42

[CVE-2026-22733](https://github.com/advisories/GHSA-mgvc-8q2h-5pgc): Spring Boot has an Authentication Bypass under Actuator CloudFoundry endpoints

Severity: HIGH

Affected packages:
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `>= 4.0.0-M1, < 4.0.4` (fix: upgrade to 4.0.4)
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `>= 3.5.0, < 3.5.12` (fix: upgrade to 3.5.12)
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `>= 3.4.0, <= 3.4.13` (no patch available)
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `>= 3.0.0, <= 3.3.13` (no patch available)
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `<= 2.7.18` (no patch available)

Files: spring-boot/pom.xml:42

### CVE-2026-22731: Spring Boot has an Authentication Bypass under Actuator Health groups paths
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** spring-boot/pom.xml:42

[CVE-2026-22731](https://github.com/advisories/GHSA-8hfc-fq58-r658): Spring Boot has an Authentication Bypass under Actuator Health groups paths

Severity: HIGH

Affected packages:
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `>= 3.4.0, <= 3.4.13` (no patch available)
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `>= 3.5.0, < 3.5.12` (fix: upgrade to 3.5.12)
  - `org.springframework.boot:spring-boot-starter-actuator` affected range: `>= 4.0.0-M1, < 4.0.4` (fix: upgrade to 4.0.4)

Files: spring-boot/pom.xml:42

### CVE-2022-1471: SnakeYaml Constructor Deserialization Remote Code Execution
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** micronaut/pom.xml:79

[CVE-2022-1471](https://github.com/advisories/GHSA-mjmj-j48q-9wg2): SnakeYaml Constructor Deserialization Remote Code Execution

Severity: HIGH

Affected packages:
  - `org.yaml:snakeyaml` affected range: `<= 1.33` (fix: upgrade to 2.0)

Files: micronaut/pom.xml:79

### CVE-2022-25857: Uncontrolled Resource Consumption in snakeyaml
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** micronaut/pom.xml:79

[CVE-2022-25857](https://github.com/advisories/GHSA-3mc7-4q67-w48m): Uncontrolled Resource Consumption in snakeyaml

Severity: HIGH

Affected packages:
  - `org.yaml:snakeyaml` affected range: `< 1.31` (fix: upgrade to 1.31)

Files: micronaut/pom.xml:79

### GHSA-2m67-wjpj-xhg9: Jackson Core: Document length constraint bypass in blocking, async, and DataInput parsers
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[GHSA-2m67-wjpj-xhg9](https://github.com/advisories/GHSA-2m67-wjpj-xhg9): Jackson Core: Document length constraint bypass in blocking, async, and DataInput parsers

Severity: HIGH

Affected packages:
  - `tools.jackson.core:jackson-core` affected range: `>= 3.0.0, <= 3.1.0` (fix: upgrade to 3.1.1)

Files: pom.xml

### CVE-2026-29062: jackson-core has Nesting Depth Constraint Bypass in `UTF8DataInputJsonParser` potentially allowing Resource Exhaustion
- **Severity:** mandatory
- **Story Points:** 1
- **Files:** pom.xml

[CVE-2026-29062](https://github.com/advisories/GHSA-6v53-7c9g-w56r): jackson-core has Nesting Depth Constraint Bypass in `UTF8DataInputJsonParser` potentially allowing Resource Exhaustion

Severity: HIGH

Affected packages:
  - `tools.jackson.core:jackson-core` affected range: `>= 3.0.0, < 3.1.0` (fix: upgrade to 3.1.0)

Files: pom.xml

## CWE Findings (Code-Level Vulnerabilities)

### CWE-477: Use of Obsolete Function
- **Category:** Code Quality
- **Severity:** optional
- **Story Points:** 1
- **Files:** tomcat/src/main/java/io/brunoborges/showmyjvm/tomcat/ShowMyJVMServlet.java

ShowMyJVMServlet.handleError() (line 49) and handlePlainTextInspect() (line 59) call e.printStackTrace() to print exception stack traces directly to stderr rather than using the injected SLF4J logger. printStackTrace() is considered an obsolete debugging practice in production server code.

### CWE-570: Expression is Always False
- **Category:** Code Quality
- **Severity:** optional
- **Story Points:** 1
- **Files:** core/src/main/java/io/brunoborges/showmyjvm/core/PrintFlagsFinal.java

In PrintFlagsFinal.readJVMFlags() the guard condition is: 'if (jvmFlags == Collections.EMPTY_LIST || jvmFlags != null)'. The field jvmFlags is null by default and is only ever assigned an ArrayList instance — never Collections.EMPTY_LIST — so the sub-expression 'jvmFlags == Collections.EMPTY_LIST' is always false and dead code. The intended guard should be 'jvmFlags != null'.

### CWE-772: Missing Release of Resource after Effective Lifetime
- **Category:** Code Quality
- **Severity:** potential
- **Story Points:** 3
- **Files:** tomcat/src/main/java/io/brunoborges/showmyjvm/tomcat/ShowMyJVMServlet.java

In ShowMyJVMServlet.handleJsonInspect() (line 64), a Jsonb instance is created via JsonbBuilder.create() but is never closed. jakarta.json.bind.Jsonb implements AutoCloseable, so it should be wrapped in a try-with-resources block to ensure its underlying resources are always released.

### CWE-543: Use of Singleton Pattern Without Synchronization in a Multithreaded Context
- **Category:** Concurrency & Synchronization
- **Severity:** potential
- **Story Points:** 5
- **Files:** core/src/main/java/io/brunoborges/showmyjvm/core/IdentifyGC.java

IdentifyGC.initHotspotMBean() (lines 96-102) implements the double-checked locking idiom to lazily initialize the singleton hotspotMBean field, but the field is declared as 'private Object hotspotMBean' without the 'volatile' modifier. Under the Java Memory Model, without volatile, the JVM may publish a partially-constructed or stale reference to other threads that observe the outer null-check passing before the synchronized block completes, defeating the singleton guarantee in a multithreaded servlet or framework context.

### CWE-821: Incorrect Synchronization
- **Category:** Concurrency & Synchronization
- **Severity:** potential
- **Story Points:** 8
- **Files:** core/src/main/java/io/brunoborges/showmyjvm/core/IdentifyGC.java

In IdentifyGC.initHotspotMBean() the double-checked locking on 'hotspotMBean' is broken because the field is not declared volatile. The outer unsynchronized read 'if (hotspotMBean == null)' is therefore not guaranteed to observe a fully-constructed object written inside the synchronized block by another thread. Per JSR-133 (Java Memory Model), the volatile keyword is required on the guarded field for double-checked locking to be safe. The synchronized block on IdentifyGC.class does provide mutual exclusion but does not provide the cross-thread visibility needed for the unsynchronized outer check.

### CWE-778: Insufficient Logging
- **Category:** Credentials & Secrets
- **Severity:** potential
- **Story Points:** 3
- **Files:** spring-boot/src/main/java/io/brunoborges/showmyjvm/springboot/JvmInspectController.java, quarkus/src/main/java/io/brunoborges/showmyjvm/quarkus/JvmInspectResource.java, micronaut/src/main/java/io/brunoborges/showmyjvm/micronaut/JvmInspectController.java, javalin/src/main/java/io/brunoborges/showmyjvm/javalin/JvmInspectJavalinHandler.java, ratpack/src/main/java/io/brunoborges/showmyjvm/ratpack/JvmInspectRatpackHandler.java, sparkjava/src/main/java/io/brunoborges/showmyjvm/sparkjava/JvmInspectSparkJavaHandler.java, tomcat/src/main/java/io/brunoborges/showmyjvm/tomcat/ShowMyJVMServlet.java

The /jvm/inspect and /jvm/inspect.json endpoints return the full set of system properties and environment variables verbatim (via ShowJVM.extractJVMDetails()). These responses may include sensitive secrets (database passwords, API tokens, etc.) present in the process environment. None of the framework controller/handler classes log incoming requests, client identifiers, or access events. There is no audit trail for who accessed sensitive JVM introspection data, violating the requirement to record security-critical events.
