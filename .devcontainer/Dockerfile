FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    bash                                 \
    git                                  \
    curl                                 \
    nodejs                               \
    golang-go                            \
    build-essential libssl-dev pkg-config\
    glibc-source                         \
    ca-certificates

# Install Rust
RUN curl https://sh.rustup.rs -sSf | bash -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"
RUN rustup target add wasm32-wasi

# Install the gopls Go Language Server, see https://github.com/golang/tools/tree/master/gopls
RUN go install golang.org/x/tools/gopls@latest

# Install Spin and required plugins
RUN curl -fsSL https://developer.fermyon.com/downloads/install.sh | bash && mv spin /usr/local/bin/
RUN spin plugin install js2wasm -y

RUN spin templates install --git https://github.com/fermyon/spin --update
