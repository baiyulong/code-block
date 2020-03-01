### Add log for WebClient

```java
WebClient webClient = WebClient.builder()
        .filter((request, next) -> {
            log.info("Request: {} {}", request.method(), request.url());
            request.headers().forEach(
                    (name, values) -> values.forEach(
                            value -> log.info("Request: {} = {}", name, value)
                    )
            );
            return next.exchange(request);
        })
        .filter(ExchangeFilterFunction.ofResponseProcessor(response -> {
            log.info("Response: status = {}", response.statusCode());
            response.headers().asHttpHeaders().forEach(
                    (name, values) -> values.forEach(
                            value -> log.info("Response: {} = {}", name, value)
                    )
            );
            return Mono.just(response);
        }))
        .build();
```
