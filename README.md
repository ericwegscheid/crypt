# crypt

This is a simple ruby module which can also be used as a command line utility to encrypt and decrypt data.

## Usage

### In your ruby code

```ruby
load './crypt'

some_string = 'please encrypt me'
secret_password = 'sssh_ima_secret'

# get your encrypted string
encrypted_string = Crypt::encrypt(some_string, secret_password)

begin
  # decrypt, raises an error if given a bad key
  decrypted_string = Crypt::decrypt(encrypted_string, secret_password)
rescue
  puts 'Bad key'
end
```

### As a command line utility

Please note if ruby is not installed at /usr/bin/ruby and whatever directory the crypt file is not in your $PATH, running the commands as see below will not work, you may have to pass the script file to ruby something like this: `$ ruby crypt -e "some text to encrypt"`.

Encrypt a simple message:
```bash
$ crypt -e "please encrypt me"
Enter key:
Re-enter key:
VqNCWgBHf6wkWyYYXlBdVe+OdYYrg2NVCTcGbWsizs6eDVHT0yg+J3Kf0pegUa2w
```

```bash
$ crypt -e --key=asdf "please encrypt me"
VqNCWgBHf6wkWyYYXlBdVe+OdYYrg2NVCTcGbWsizs6eDVHT0yg+J3Kf0pegUa2w
```

Decrypt a message:
```bash
$ crypt -d VqNCWgBHf6wkWyYYXlBdVe+OdYYrg2NVCTcGbWsizs6eDVHT0yg+J3Kf0pegUa2w
Enter key:
Re-enter key:
please encrypt me
```

```bash
$ crypt -d --key=asdf VqNCWgBHf6wkWyYYXlBdVe+OdYYrg2NVCTcGbWsizs6eDVHT0yg+J3Kf0pegUa2w
please encrypt me
```

Encrypting and decrypting files:
```bash
$ crypt -e some-file.txt encrypted.txt
Enter key:
Re-enter key:
Success!

```
```bash
$ crypt -d encrypted.txt some-file.txt
Enter key:
Re-enter key:
Success!
```

Encrypting and decrypting directories:
```bash
$ tar -zcvf some_directory.tar.gz some_directory/
$ crypt -e some_directory.tar.gz .secret-fle
Enter key:
Re-enter key:
Success!

```
```bash
$ crypt -d .secret-file some_directory.tar.gz
Enter key:
Re-enter key:
Success!
```
