# E-Voting Using Bloakc Chain

**An e-voting system based on blockchain using ring signature**

## About the Project

BlockVotes is a secure electronic voting system that leverages blockchain technology and ring signatures to provide a transparent, complete, and verifiable voting experience. This system addresses the security concerns typically associated with digital voting by implementing blockchain's immutable ledger and cryptographic techniques.

### Why BlockVotes?

Electronic voting systems offer significant benefits to all election stakeholders:
- **For administrators**: Streamlined election operations and management
- **For voters**: Convenient voting from anywhere, anytime
- **For everyone**: Enhanced transparency, accuracy, and security

### Key Features

- **Transparency**: All transactions are recorded on a public blockchain
- **Completeness**: Only authorized voters can cast votes, and all votes are correctly counted
- **Verifiability**: Voters can verify that their votes have been properly recorded
- **Security**: Utilizes ring signatures for anonymous yet verifiable voting
- **Decentralization**: No single point of failure or control

### How It Works

BlockVotes uses blockchain technology combined with ring signatures:

1. **Blockchain Implementation**: Creates an immutable, cumulative ledger using OP_RETURN to mark transactions
2. **Ring Signature**: Provides anonymity while ensuring validity of votes
   - A group of entities each have public/private key pairs
   - A ring signature is created as: σ = (m, Si, P1, P2, ..., Pn)
   - Anyone can verify the signature's validity using the public keys

## Tech Stack

The system utilizes the following technologies:

- **Backend**: PHP 7.1+ with GMP extension
- **Database**: MySQL 5.7+
- **Web Server**: Apache 2.4+ or Nginx 1.12+
- **Dependencies**: Managed via Composer
- **Cryptography**: Elliptic Curve Digital Signature Algorithm (ECDSA)
- **Architecture**: Built on blockchain principles with ring signatures

## How to Run the Project

### System Requirements

- **Operating System**: Mac OS X, Linux, or Windows
- **Web Server**: Apache 2.4.27+ or Nginx 1.12.1+
- **Database**: MySQL 5.7.19+ (at least 5.4)
- **PHP**: 7.1.8+ (at least 7.0)
- **PHP Extensions**: php7.0-gmp
- **Package Manager**: Composer

### Setup Instructions

#### 1. Install PHP-GMP Extension

**For Ubuntu:**
```
sudo apt-get install php7.0-gmp
```
Add to php.ini:
```
extension=php_gmp.so
```

**For Mac OS X:**
```
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/homebrew-php
brew install php71
brew install php71-gmp
```
Add to php.ini:
```
extension=php_gmp.so
```

**For Windows:**
Uncomment `;extension=php_gmp.dll` in `php.ini`

#### 2. Configure Web Server

**Apache Configuration:**
Ensure `.htaccess` and `index.php` are in the same public-accessible directory.
The `.htaccess` file should contain:
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.php [QSA,L]
```

Make sure your Apache virtual host is configured with:
```
AllowOverride All
```

**Nginx Configuration:**
Create a virtual host configuration like this:
```
server {
    listen 80;
    server_name example.com;
    index index.php;
    error_log /path/to/example.error.log;
    access_log /path/to/example.access.log;
    root /path/to/public;

    location / {
        try_files $uri /index.php$is_args$args;
    }

    location ~ \.php {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param SCRIPT_NAME $fastcgi_script_name;
        fastcgi_index index.php;
        fastcgi_pass 127.0.0.1:9000;
    }
}
```

Note: The `public` directory is the entrance point of the system.

#### 3. Configure BlockVotes

Create a `.env` file in the project root directory with the following content:
```
DB_DRIVER=mysql
DB_HOST=127.0.0.1
DB_DATABASE=blockvotes
DB_USERNAME=root
DB_PASSWORD=
DB_PORT=3306

STMP_SERVER=smtp.gmail.com
STMP_PORT=465
STMP_USERNAME=xxx@gmail.com
STMP_PASSWORD=password
```

#### 4. Set Up Database

Import the sample SQL file [`blockvotes.sql`](https://gist.github.com/yfgeek/75c53298d59f335c65a6cc03703ec02e) to MySQL.

#### 5. Install Dependencies

Run Composer to install all dependencies:
```
php composer.phar install
```
## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Contact
For any queries, reach out at rcrathod13@gmail.com or open an issue on GitHub!
