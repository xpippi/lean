## Setup instruction

### Method 1 - Clone this repo directly

1. Clone this repo:

	```bash
	rm -rf package/groundhello
	git clone --depth=1 https://github.com/xpippi/groundhello.git package/groundhello
	```

2. Pull upstream commits:

	```bash
	git -C package/groundhello pull
	```

- Remove

  ```bash
  rm -rf package/groundhello
  ```

### Method 2 - Add this repo as a git submodule

1. Add new submodule:

	```bash
	rm -rf package/groundhello
	git submodule add -f --name groundhello https://github.com/xpippi/groundhello.git package/groundhello
	```

2. Pull upstream commits:

	```bash
	git submodule update --remote package/groundhello
	```

- Remove

  ```bash
  git submodule deinit -f package/groundhello
  git rm -f package/groundhello
  git reset HEAD .gitmodules
  rm -rf .git/modules{/,/package/}groundhello
  ```

### Method 3 - Add this repo as an OpenWrt feed

1. Add new feed:

	```bash
	sed -i "/groundhello/d" "feeds.conf.default"
	echo "src-git groundhello https://github.com/xpippi/groundhello.git" >> "feeds.conf.default"
	```

2. Pull upstream commits:

	```bash
	./scripts/feeds update groundhello
	./scripts/feeds install -a -f -p groundhello
	```

- Remove

  ```bash
  sed -i "/groundhello/d" "feeds.conf.default"
  ./scripts/feeds clean
  ./scripts/feeds update -a
  ./scripts/feeds install -a
  ```

### Note

#### ⚠ For OpenWrt 21.02 or lower version
You have to manually upgrade Golang toolchain to [1.19](https://github.com/openwrt/packages/tree/openwrt-22.03/lang/golang) or higher to compile Xray-core.

e.g.:

```bash
./scripts/feeds update packages
rm -rf feeds/packages/lang/golang
svn co https://github.com/openwrt/packages/branches/openwrt-22.03/lang/golang feeds/packages/lang/golang
```
