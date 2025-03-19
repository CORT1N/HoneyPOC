# 🛡️ Simple Containerized Honeypot POC 🕵️‍♂️

This project sets up a honeypot using various technologies to simulate a vulnerable environment. The setup includes an Nginx reverse proxy, a WordPress site, a database, an SMTP server, and an SSH server.

## 🚀 Setup Instructions

### 1️⃣ Clone the Repository

```sh
git clone https://github.com/CORT1N/HoneyPOC
cd HoneyPOC
```

### 2️⃣ Start the Services

```sh
docker compose up -d
```

### 3️⃣ Verify the Services Are Running

```sh
docker compose ps
```

---

## 🔍 Testing Endpoints

### 🌐 HTTP (Port 80)

- **Description**: Redirects HTTP traffic to HTTPS.
- **Test**:

    ```sh
    curl -I http://localhost
    ```

- **Expected Result**: HTTP 301 redirect to HTTPS.

### 🔒 HTTPS (Port 443)

- **Description**: Serves the WordPress site over HTTPS.
- **Test**:

    ```sh
    curl -k https://localhost
    ```

- **Expected Result**: HTML content of the WordPress site.

### 🐄 MySQL (Port 3306)

- **Description**: Database server for WordPress.
- **Test**:

    ```sh
    mysql -h 127.0.0.1 -u Tf38izWsvL2VsBjrvwRzw06zavjFCghc -p
    ```

    or

    ```sh
    telnet localhost 3306
    ```

- **Expected Result**: MySQL prompt after entering the password. (1) or MariaDB server banner. (2)

### 📧 SMTP (Port 25)

- **Description**: SMTP server for sending emails.
- **Test**:

    ```sh
    telnet localhost 25
    ```

- **Expected Result**: SMTP server banner.

### 🖥️ SSH (Port 2222)

- **Description**: SSH server for remote access.
- **Test**:

    ```sh
    ssh attacker@localhost -p 2222
    ```

- **Expected Result**: SSH login prompt.

---

## 📝 Log Verification

All logs are stored in the `logs` directory. Verify that logs are being written correctly by checking the following files:

- **📝 Nginx Access Logs**: `logs/unified_access.log`
- **⚠️ Nginx Error Logs**: `logs/error.log`

### 🔎 Example Log Check

1️⃣ **Access the Nginx access log**:

```sh
tail -f logs/unified_access.log
```

2️⃣ **Generate traffic**:

```sh
curl -k https://localhost
```

3️⃣ **Verify the log entry**:

- You should see a new entry in `unified_access.log` corresponding to the request.

---

## 🔑 Command Used to Generate SSL

To generate a self-signed SSL certificate for the honeypot, use the following command:

```sh
mkdir -p ./ssl && openssl req -x509 -nodes -days 1 -newkey rsa:2048 -keyout ./ssl/server.key -out ./ssl/server.crt -subj "/CN=localhost"
```

---

## ⚠️ Disclaimer – Educational Purpose Only 🚨

This project is **strictly** intended for **educational and cybersecurity research purposes**. Using this honeypot in uncontrolled environments or for malicious activities is **illegal** and may lead to prosecution.

👨‍💻 **Use this project responsibly!** 🚫
