```
-- Created by Vertabelo (http://vertabelo.com)
-- Last modification date: 2024-05-03 22:43:29.651

-- tables
-- Table: accessories
CREATE TABLE accessories (
    id int  NOT NULL,
    name varchar(16)  NOT NULL,
    brand varchar(16)  NOT NULL,
    price double  NOT NULL,
    image_url varchar(255)  NOT NULL,
    CONSTRAINT accessories_pk PRIMARY KEY (id)
);

-- Table: accessories_per_bike
CREATE TABLE accessories_per_bike (
    accessories_id int  NOT NULL,
    bikes_id int  NOT NULL,
    CONSTRAINT accessories_per_bike_pk PRIMARY KEY (accessories_id,bikes_id)
);

-- Table: bike_posts
CREATE TABLE bike_posts (
    id int  NOT NULL,
    description text  NOT NULL,
    price_per_hour double  NOT NULL,
    is_active bool  NOT NULL,
    bikes_id int  NOT NULL,
    CONSTRAINT bike_posts_pk PRIMARY KEY (id)
);

-- Table: bikes
CREATE TABLE bikes (
    id int  NOT NULL,
    name varchar(16)  NOT NULL,
    brand varchar(16)  NOT NULL,
    image_url varchar(255)  NOT NULL,
    profiles_id int  NOT NULL,
    CONSTRAINT bikes_pk PRIMARY KEY (id)
);

-- Table: issue_reports
CREATE TABLE issue_reports (
    id int  NOT NULL,
    title varchar(32)  NOT NULL,
    description text  NOT NULL,
    proof_image_url varchar(255)  NOT NULL,
    resolution varchar(255)  NOT NULL,
    created_at date  NOT NULL,
    updated_at date  NOT NULL,
    rents_id int  NOT NULL,
    report_status_id int  NOT NULL,
    CONSTRAINT issue_reports_pk PRIMARY KEY (id)
);

-- Table: privileges
CREATE TABLE privileges (
    id int  NOT NULL,
    name varchar(24)  NOT NULL,
    CONSTRAINT privileges_pk PRIMARY KEY (id)
);

-- Table: profile_privileges
CREATE TABLE profile_privileges (
    profiles_id int  NOT NULL,
    privileges_id int  NOT NULL,
    CONSTRAINT profile_privileges_pk PRIMARY KEY (profiles_id,privileges_id)
);

-- Table: profiles
CREATE TABLE profiles (
    id int  NOT NULL,
    profile_picture_url varchar(255)  NOT NULL,
    users_id int  NOT NULL,
    CONSTRAINT profiles_pk PRIMARY KEY (id)
);

-- Table: rents
CREATE TABLE rents (
    id int  NOT NULL,
    starting_date date  NOT NULL,
    ending_date date  NULL,
    price double  NOT NULL,
    bikes_id int  NOT NULL,
    profiles_id int  NOT NULL,
    CONSTRAINT rents_pk PRIMARY KEY (id)
);

-- Table: report_status
CREATE TABLE report_status (
    id int  NOT NULL,
    status varchar(50)  NOT NULL,
    CONSTRAINT report_status_pk PRIMARY KEY (id)
);

-- Table: roles
CREATE TABLE roles (
    id int  NOT NULL,
    name varchar(24)  NOT NULL,
    CONSTRAINT roles_pk PRIMARY KEY (id)
);

-- Table: travel_datas
CREATE TABLE travel_datas (
    id int  NOT NULL,
    distance_in_km double  NOT NULL,
    rating_exp int  NOT NULL,
    rents_id int  NOT NULL,
    CONSTRAINT travel_datas_pk PRIMARY KEY (id)
);

-- Table: user_roles
CREATE TABLE user_roles (
    roles_id int  NOT NULL,
    users_id int  NOT NULL,
    CONSTRAINT user_roles_pk PRIMARY KEY (roles_id,users_id)
);

-- Table: users
CREATE TABLE users (
    id int  NOT NULL,
    username varchar(16)  NOT NULL,
    email varchar(16)  NOT NULL,
    password varchar(255)  NOT NULL,
    first_name varchar(12)  NOT NULL,
    last_name varchar(12)  NOT NULL,
    CONSTRAINT users_pk PRIMARY KEY (id)
);

-- foreign keys
-- Reference: Table_6_privileges (table: profile_privileges)
ALTER TABLE profile_privileges ADD CONSTRAINT Table_6_privileges FOREIGN KEY Table_6_privileges (privileges_id)
    REFERENCES privileges (id);

-- Reference: Table_6_profiles (table: profile_privileges)
ALTER TABLE profile_privileges ADD CONSTRAINT Table_6_profiles FOREIGN KEY Table_6_profiles (profiles_id)
    REFERENCES profiles (id);

-- Reference: Table_8_roles (table: user_roles)
ALTER TABLE user_roles ADD CONSTRAINT Table_8_roles FOREIGN KEY Table_8_roles (roles_id)
    REFERENCES roles (id);

-- Reference: Table_8_users (table: user_roles)
ALTER TABLE user_roles ADD CONSTRAINT Table_8_users FOREIGN KEY Table_8_users (users_id)
    REFERENCES users (id);

-- Reference: accessories_per_bike_accessories (table: accessories_per_bike)
ALTER TABLE accessories_per_bike ADD CONSTRAINT accessories_per_bike_accessories FOREIGN KEY accessories_per_bike_accessories (accessories_id)
    REFERENCES accessories (id);

-- Reference: accessories_per_bike_bikes (table: accessories_per_bike)
ALTER TABLE accessories_per_bike ADD CONSTRAINT accessories_per_bike_bikes FOREIGN KEY accessories_per_bike_bikes (bikes_id)
    REFERENCES bikes (id);

-- Reference: bike_posts_bikes (table: bike_posts)
ALTER TABLE bike_posts ADD CONSTRAINT bike_posts_bikes FOREIGN KEY bike_posts_bikes (bikes_id)
    REFERENCES bikes (id);

-- Reference: bikes_profiles (table: bikes)
ALTER TABLE bikes ADD CONSTRAINT bikes_profiles FOREIGN KEY bikes_profiles (profiles_id)
    REFERENCES profiles (id);

-- Reference: issue_reports_rents (table: issue_reports)
ALTER TABLE issue_reports ADD CONSTRAINT issue_reports_rents FOREIGN KEY issue_reports_rents (rents_id)
    REFERENCES rents (id);

-- Reference: issue_reports_report_status (table: issue_reports)
ALTER TABLE issue_reports ADD CONSTRAINT issue_reports_report_status FOREIGN KEY issue_reports_report_status (report_status_id)
    REFERENCES report_status (id);

-- Reference: profiles_users (table: profiles)
ALTER TABLE profiles ADD CONSTRAINT profiles_users FOREIGN KEY profiles_users (users_id)
    REFERENCES users (id);

-- Reference: rents_bikes (table: rents)
ALTER TABLE rents ADD CONSTRAINT rents_bikes FOREIGN KEY rents_bikes (bikes_id)
    REFERENCES bikes (id);

-- Reference: rents_profiles (table: rents)
ALTER TABLE rents ADD CONSTRAINT rents_profiles FOREIGN KEY rents_profiles (profiles_id)
    REFERENCES profiles (id);

-- Reference: travel_datas_rents (table: travel_datas)
ALTER TABLE travel_datas ADD CONSTRAINT travel_datas_rents FOREIGN KEY travel_datas_rents (rents_id)
    REFERENCES rents (id);

-- End of file.

```
