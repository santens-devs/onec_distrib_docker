FROM alpine as build
WORKDIR /opt/onec
RUN unlink ./platform 2>/dev/null ; ln -s -r ./8/3/17/2306/x86_64 ./platform
FROM scratch as production
COPY --from=build /opt /
CMD ["/opt/onec/platform"]
