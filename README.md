# Gator

The Blog Aggregator allows users to track blog feeds from the internet. Users can register to follow feed(s), retrieve their content, and store it locally to read at their convenience later.

## Requirements:
- [Go](#go-setup)
- [Go Dependencies](#go-dependencies)
- [PostgreSQL Database](#postgresql-database)
- [Database Setup](#database-setup)

## Go Setup
Run the following commands to install go:
```
curl -sS https://webi.sh/golang | sh
echo 'export PATH=$PATH:$HOME/.local/opt/go/bin' >> ~/.bashrc
source ~/.bashrc

# verify installation
go version
```

# Go Dependencies
Intall the followin Go Packages
```
go install github.com/pressly/goose/v3/cmd/goose@latest
go install github.com/sqlc-dev/sqlc/cmd/sqlc@latest
```

## PostgreSQL Database
Run the following commands to install Postgres:
```
sudo apt update
sudo apt install postgresql postgresql-contrib -y

# verify installation
psql --version

# set postgress password, follow the promps
sudo passwd postgres

# start the service
sudo service postgresql start

# connect to the postgres
sudo -u postgres psql

```
Set up the Gator database
```
CREATE DATABASE gator;
\c gator
ALTER USER postgres PASSWORD 'postgres';

```

# Running The Program
Before staring you will need to set up you database, to do so run the following:
```
sql/schema/
goose postgres postgres://postgres:postgres@localhost:5432/gator up
cd ../..
```
Once the is set up you can run use by running:
```
go run . command
```
All these command are availble:

- Register a User: `go run . start register <username>`
- Login: `go run . start login <username>`
- List All Users: `go run . start users`
- List All Blog Feeds: `go run . start feeds`
- Follow a Blog Feed: `go run . start follow <url_to_blog_feed>`
- Unfollow a Feed: `go run . start unfollow <url_to_blog_feed>`
- Add a Blog Feed: `go run . start addfeed "<feed_name>" "<url_to_blog_feed>"`
- View Followed Feeds (Logged-In User): `go run . start following`
- Store Blog Feeds: `go run . start agg <timeframe>`
- Display Blog Feeds: `go run . start browse <number>`

> `timeframe` must be a number with a unit: `ms`, `s`, `m`, or `h` (e.g., `1m`)