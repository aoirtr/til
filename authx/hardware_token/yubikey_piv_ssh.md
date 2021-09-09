# yubikeyでのSSH認証

## 環境

* windows 10

## 参考

[秘密鍵、管理してますか? YubiKeyで鍵の一元管理とSSH接続、２段階認証の高速化を試す \- Qiita](https://qiita.com/dseg/items/77d77467970b1b510285#%E6%9C%80%E5%BE%8C%E3%81%AB-pin%E3%81%AE%E8%A8%AD%E5%AE%9A)

## install

* [yubico\-piv\-tool](https://developers.yubico.com/yubico-piv-tool/)
  * [Releases](https://developers.yubico.com/yubikey-manager-qt/Releases/)
* [Releases · OpenSC/OpenSC](https://github.com/OpenSC/OpenSC/releases/)

### 以下では使わないがとりあえずいれたもの

* [YubiKey Manager \| Yubico](https://www.yubico.com/support/download/yubikey-manager/)

## コマンド

### 9aスロットに証明書を発行

```powershell
yubico-piv-tool -a status
#=> Version:        5.1.2
#=> Serial Number:  XXXXXXXXX
#=> CHUID:  No data available
#=> CCC:    No data available
#=> PIN tries left: 3

yubico-piv-tool -s 9a -a generate -o public.pem -A ECCP384
#=> Successfully generated a new private key.

yubico-piv-tool -a verify-pin -P 123456 -a selfsign-certificate -s 9a -S "/CN=SSH key/" -i public.pem -o cert.pem
#=> Successfully verified PIN.
#=> Successfully generated a new self signed certificate.

yubico-piv-tool -a import-certificate -s 9a -i cert.pem
#=> Successfully imported a new certificate.

cd "C:\Program Files\OpenSC Project\OpenSC\tools"

.\pkcs15-tool.exe --read-ssh-key 1
#=> Using reader with a card: Yubico YubiKey OTP+FIDO+CCID 0
#=> ecdsa-sha2-nistp384 XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX== PIV AUTH pubkey
```

### GPG設定

* GPG忘れてるし100％理解してない

```powershell
gpg --card-status

gpg --card-edit
gpg/card> admin
gpg/card> generate

$SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"

gpg-connect-agent /bye
ssh-add -L

gpg-connect-agent killagent /bye
gpg-connect-agent /bye

ssh-add -L

gpg --card-status
# ...
# General key info..: pub  rsa2048/XXXXXXXXXX YYYY-MM-DD name <mail@example.com>
# ...

gpg --export-ssh-key XXXXXXXXXX > ssh_auth_key.pub

cat .\ssh_auth_key.pub
```
