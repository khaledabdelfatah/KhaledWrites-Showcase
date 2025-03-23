# **Keycloak Identity and Access Management**

Keycloak is an open-source identity and access management solution that provides single sign-on (SSO) capabilities for web applications and services. It allows you to secure your applications by providing centralized authentication, authorization, and user management.

## **How to Install Keycloak 21.1.2**

You can install Keycloak 21.1.2 using either the distribution file or Docker:

### **Using the Distribution File**

1. Download Keycloak:

    ```bash
    export KC_VERSION=21.1.2
    curl -LO https://github.com/keycloak/keycloak/releases/download/"${KC_VERSION}"/keycloak-"${KC_VERSION}".zip

    ```
2. Unpack the archive:

    ```bash
    unzip keycloak-${KC_VERSION}.zip
    ```

3. Navigate to the directory:

    ```bash
    cd keycloak-${KC_VERSION}
    ```
4. Start the server in development mode:

    ```bash
    KEYCLOAK_ADMIN=admin KEYCLOAK_ADMIN_PASSWORD=admin ./bin/kc.sh start-dev
    ```
5. Access the Admin Console at [http://localhost:8080](http://localhost:8080).

### **Using Docker**

1. Run the following command:

    ```bash
    docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:21.1.2 start-dev
    ```


2. Access the Admin Console at [http://localhost:8080](http://localhost:8080).

## **How to Define a New Realm**

A realm in Keycloak is a security administrative area where you manage users, credentials, roles, and groups. To define a new realm:

1. Log in to the Keycloak Admin Console.
2. Click on the dropdown menu next to Master Realm in the top-left corner.
3. Select Add Realm.
4. Specify a name for your realm (e.g., myrealm) and click Create

## **How to Define a New Client** 

A client in Keycloak represents an application that can request authentication. To create a new client:

1. Navigate to your realm (e.g., myrealm) in the Admin Console.
2. Select Clients from the left-hand menu.
3. Click Create.
4. Fill in the following details:
    - Client ID: A unique identifier for the client (e.g., myclient).
    - Client Protocol: Select openid-connect.
    - Access Type: Choose between public or confidential based on your requirements.
5. Save and configure additional settings such as redirect URIs, web origins, and more.

## **How to Create Realm Roles**

Realm roles in Keycloak are global roles that can be assigned to users within a realm. To create realm roles:

1. Go to your realm (myrealm) in the Admin Console.
2. Click on Roles in the left-hand menu.
3. Click Add Role.
4. Enter a name for your role (e.g., user-role) and optionally provide a description.
5. Save the role.

## **How to Create a New User and Assign Realm Roles**

To create a user and assign roles:

1. Navigate to your realm (myrealm) in the Admin Console.
2. Click on Users in the left-hand menu, then select Add User.
3. Fill out user details such as username, first name, last name, and email, then click Save.
4. Set a password for the user by selecting the Credentials tab, entering a password, and enabling temporary or permanent options.
5. Assign roles:
    - Go to the user's profile and click on Role Mappings.
    - Select roles from either realm-level or client-level roles (e.g., user-role).
    - Save changes.

---
**References**:
- [Downloading Keycloak](https://www.keycloak.org/downloads)
- [Keycloak Authorization Services](https://www.keycloak.org/docs/latest/authorization_services/index.html) 

