# LibreWolf uBO policy pacman hook

This hook patches LibreWolf's enterprise policy after `librewolf` or
`librewolf-bin` is installed or upgraded.

It changes:

```json
"uBlock0@raymondhill.net": {
  "install_url": "...latest.xpi",
  "installation_mode": "normal_installed",
  "private_browsing": true
}
```

to:

```json
"uBlock0@raymondhill.net": {
  "installation_mode": "allowed"
}
```

Install:

```sh
sudo install -Dm755 librewolf-disable-ubo-policy /usr/local/bin/librewolf-disable-ubo-policy
sudo install -Dm644 librewolf-disable-ubo-policy.hook /etc/pacman.d/hooks/librewolf-disable-ubo-policy.hook
```

Run once immediately:

```sh
sudo /usr/local/bin/librewolf-disable-ubo-policy
```

Verify:

```sh
jq '.policies.ExtensionSettings["uBlock0@raymondhill.net"]' /usr/lib/librewolf/distribution/policies.json
```
