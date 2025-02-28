# Automatizacion-Sql-Oracle

CREATE USER user_script IDENTIFIED BY "123456";

GRANT "CONNECT" TO user_script;
GRANT "RESOURCE" TO user_script;


CREATE TABLE users (
    id VARCHAR2(20) PRIMARY KEY,
    updated_at DATE,
    created_at DATE,
    email VARCHAR2(30) UNIQUE NOT NULL,
    password VARCHAR2(25) NOT NULL,
    first_name VARCHAR2(20),
    last_name VARCHAR2(20)
);

CREATE TABLE state (
    id VARCHAR2(20) PRIMARY KEY,
    updated_at DATE,
    created_at DATE,
    name VARCHAR2(30) NOT NULL
);

CREATE TABLE city (
    id VARCHAR2(20) PRIMARY KEY,
    updated_at DATE,
    created_at DATE,
    state_id VARCHAR2(20) NOT NULL,
    name VARCHAR2(30) NOT NULL
);

CREATE TABLE place (
    id VARCHAR2(20) PRIMARY KEY,
    updated_at DATE,
    created_at DATE,
    user_id VARCHAR2(20) NOT NULL,
    name VARCHAR2(30) NOT NULL,
    city_id VARCHAR2(20) NOT NULL,
    description VARCHAR2(100),
    number_rooms INTEGER DEFAULT 0,
    number_bathrooms INTEGER DEFAULT 0,
    max_guest INTEGER DEFAULT 0,
    price_by_night INTEGER DEFAULT 0,
    latitude FLOAT,
    longitude FLOAT
);

CREATE TABLE review (
    id VARCHAR2(20) PRIMARY KEY,
    updated_at DATE,
    created_at DATE,
    user_id VARCHAR2(20) NOT NULL,
    place_id VARCHAR2(20) NOT NULL,
    text VARCHAR2(200) NOT NULL
);

CREATE TABLE amenity (
    id VARCHAR2(20) PRIMARY KEY,
    updated_at DATE,
    created_at DATE,
    name VARCHAR2(30) NOT NULL
);

CREATE TABLE placeamenity (
    amenity_id VARCHAR2(20) NOT NULL,
    place_id VARCHAR2(20) NOT NULL,
    PRIMARY KEY (amenity_id, place_id)
);


ALTER TABLE city ADD CONSTRAINT fk_city_state FOREIGN KEY (state_id) REFERENCES state(id);
ALTER TABLE place ADD CONSTRAINT fk_place_users FOREIGN KEY (user_id) REFERENCES users(id);
ALTER TABLE place ADD CONSTRAINT fk_place_city FOREIGN KEY (city_id) REFERENCES city(id);
ALTER TABLE review ADD CONSTRAINT fk_review_users FOREIGN KEY (user_id) REFERENCES users(id);
ALTER TABLE review ADD CONSTRAINT fk_review_place FOREIGN KEY (place_id) REFERENCES place(id);
ALTER TABLE placeamenity ADD CONSTRAINT fk_placeamenity_amenity FOREIGN KEY (amenity_id) REFERENCES amenity(id);
ALTER TABLE placeamenity ADD CONSTRAINT fk_placeamenity_place FOREIGN KEY (place_id) REFERENCES place(id);