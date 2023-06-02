### Gradle 설치 (Mac OS 기준)
- HomeBrew를 통해 설치
- HomeBrew가 없다면 [HomeBrew 설치](https://brew.sh/index_ko)를 통해 설치
- 아래 두가지 명령어를 입력해야 brew 명령어를 사용할 수 있음
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

echo 'export PATH="/usr/local/opt/openjdk/bin:$PATH"' >> ~/.bash_profile 
eval "$(/opt/homebrew/bin/brew shellenv)"
```
- HomeBrew 설치 후 아래 명령어를 통해 Gradle 설치
- 버전확인
```bash
$ brew install gradle

$ gradle -v
```

- HomeBrew 설치 후 아래 명령어를 통해 Gradle 설치
