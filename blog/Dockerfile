
# Build Stage
FROM rustlang/rust:nightly

# Installation de la bibliothèque libpq
RUN apt-get update && apt-get install -y libpq-dev

RUN cargo install diesel_cli --no-default-features --features postgres

WORKDIR /blog
# Copie du code source dans l'image
COPY . .
RUN cargo install --path .

RUN cp /usr/local/cargo/bin/blog ./blog
# Compilation de l'application


# Run Diesel Migrations and start the application
CMD diesel migration run &&  ./blog
