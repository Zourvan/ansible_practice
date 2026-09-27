# ansible wordpress

پروژه ساده ansible برای نصب wordpress روی دو تا سرور ubuntu.

- web01 = nginx + php + wordpress
- db01 = mysql

## قبل از اجرا

1. ansible نصب باشه
2. به سرورها با ssh وصل بشی (user: ubuntu)
3. IP ها رو تو `inventory/hosts.ini` و `inventory/group_vars/all.yml` عوض کن

## نصب ansible و collection ها

```bash
sudo apt update
sudo apt install -y ansible
cd ansible-wordpress-stack
ansible-galaxy collection install -r requirements.yml
```

## پسورد دیتابیس (vault)

```bash
cp inventory/group_vars/vault.yml.example inventory/group_vars/vault.yml
# پسورد رو عوض کن
ansible-vault encrypt inventory/group_vars/vault.yml
```

## اجرا

```bash
ansible all -m ping
ansible-playbook playbooks/site.yml --ask-vault-pass
```

بعد برو تو مرورگر: `http://IP_WEB`

## ساختار

```
inventory/     -> لیست سرورها و متغیرها
playbooks/     -> playbook ها
roles/         -> کارای هر بخش (nginx, php, mysql, ...)
```

اگه ubuntu 22.04 داری، تو `webservers.yml` نسخه php رو به 8.1 عوض کن.
