### How to sent http request of XML by WebClient

#### Dependencies

```java
dependencies {
    compile 'javax.xml.bind:jaxb-api:2.3.1'
    compile 'org.glassfish.jaxb:jaxb-runtime:2.3.2'
}
```

#### Build WebClient Request

```java
WebClient.create()
        .post()
        .uri(this.url)
        .headers(headers -> headers.setBasicAuth(this.username, this.password))
        .contentType(MediaType.APPLICATION_XML)
        .body(Mono.just(soapEnvelope), SoapEnvelope.class)
        .retrieve()
        .bodyToMono(Output.class)
```
