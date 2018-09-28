# Build Ship
FROM avcosystems/golang-node as build-step
ENV GOPATH=/go
RUN apt-get install bzip2
COPY .git /go/src/github.com/replicatedhq/ship/.git
COPY hack /go/src/github.com/replicatedhq/ship/hack
COPY web/app/build /go/src/github.com/replicatedhq/ship/web/app/build
COPY cmd /go/src/github.com/replicatedhq/ship/cmd
COPY pkg /go/src/github.com/replicatedhq/ship/pkg
COPY vendor /go/src/github.com/replicatedhq/ship/vendor
COPY Makefile /go/src/github.com/replicatedhq/ship/Makefile
WORKDIR /go/src/github.com/replicatedhq/ship
RUN make build-ci-cypress

FROM cypress/browsers:chrome67

WORKDIR /repo
COPY Cypress /repo/Cypress
ENV CYPRESS_CACHE_FOLDER=/repo/Cypress
ADD web/app/cypress.json /repo/web/app/cypress.json
ADD web/app/cypress /repo/web/app/cypress
ADD Makefile /repo/Makefile
RUN CYPRESS_INSTALL_BINARY=0 CI=true npm i cypress@3.1.0
COPY --from=build-step /go/src/github.com/replicatedhq/ship/bin/ship /repo/bin/ship
CMD ["make", "cypress_base"]
