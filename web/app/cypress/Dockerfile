FROM cypress/browsers:chrome67

WORKDIR /repo
COPY Cypress /repo/Cypress
ENV CYPRESS_CACHE_FOLDER=/repo/Cypress
ADD web/app/cypress.json /repo/web/app/cypress.json
ADD web/app/cypress /repo/web/app/cypress
ADD Makefile /repo/Makefile
RUN CYPRESS_INSTALL_BINARY=0 CI=true npm i cypress@3.1.0
COPY bin/ship /repo/bin/ship
CMD ["make", "cypress_base"]
