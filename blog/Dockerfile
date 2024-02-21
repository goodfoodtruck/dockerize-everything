# Build Stage
FROM rustlang/rust:nightly as builder

WORKDIR /blog

# Installation de la bibliothèque libpq
RUN apt-get update && apt-get install -y libpq-dev

# Copie du code source dans l'image
COPY . .
RUN cargo install --path .

RUN cp /usr/local/cargo/bin/blog ./blog
# Compilation de l'application
RUN cargo install diesel_cli --no-default-features --features postgres

# Spécifiez les mêmes informations d'identification que pour la base de données
ENV DATABASE_URL=postgres://admin:admin@db:5432/blog

RUN diesel migration run
# Run Diesel Migrations and start the application
CMD  ["sh","./blog"]
