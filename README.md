<div align="center">

  <h1><code>rust-MSYS2-windows</code></h1>

  <strong>The compilation of failures using <a href="https://www.rust-lang.org">RUST</a> X <a href="https://www.msys2.org">MSYS2</a>.</strong>
</div>

## About

- 원래, [git for windows sdk](https://github.com/git-for-windows/build-extra/releases)를 잘 사용하고 있었다.
- 근데, 갑자기 `그곳`에서 `cmd`고 `powershell`이고 다 막아버려서 윈도우즈에서 개발하기가 매우 불편해졌다...
- [WebAssembly Studio](https://webassembly.studio/) 같은 클라우드 서비스 기반 IDE도 찾아보고, 그냥 VS설치해서 MSVC기반으로 개발해버릴까 생각도 해보았지만, 추후 각종 설치 파일들 관리할 걸 생각해보니 암담해졌다.
- 좌우간, 러스트로 작업하는데 있어서 통합된 개발 환경을 만들고자 삽질한 경험들을 여기에 올려본다.
- 결국 종착역은 MSYS2 + GCC + RUST + WASM

## 삽질 내역

- [x] `gcc.exe` 못 찾겠다. (`gcc` 미설치)
- [x] `cc NONE` 오류 (`.cargo/config` 파일 작성)
- [x] `x86_64` 오류 `gcc.exe` 못 찾겠다와 관련 있음 (`mingw-w64-x86_64-toolchain` 설치하면 됨, 그리고 `mingw64.exe` 사용해야함) 
- [x] `cargo` 못 찾겠다.

```
[target.x86_64-pc-windows-gnu]
linker = "C:\msys2\mingw64\bin\gcc.exe"
ar = "C:\msys2\mingw64\bin\ar.exe"
```

## 옳바른 설치 순서

- MSYS2 설치
- `mingw64.exe` 실행
- `pacman -Ss git mingw-w64-x86-_64-toolchain`
- 'curl https://sh.rustup.rs -sSf | sh`
- `export PATH=$PATH:$USERPROFILE/.cargo/bin`
- `vim $USERPROFILE/.cargo/cofig`
