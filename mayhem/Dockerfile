FROM fuzzers/go-fuzz:1.2.0 as builder

ARG project='gostatsd'
ARG fuzzTargetPath='internal/lexer'

ADD . ${project}
WORKDIR ${project}
RUN GO_ENABLED=0 go-fuzz-build -libfuzzer -o /lexer_fuzz.a ./${fuzzTargetPath}
RUN clang -fsanitize=fuzzer /lexer_fuzz.a -o /lexer_fuzz.libfuzzer

FROM ubuntu:20.04
COPY --from=builder /lexer_fuzz.libfuzzer /