# 개요
* 도커가 설치된 vagrant


# 설정
* 사용하지 않는 IP를 config.yml에 설정
* 메모리와 cpu설정
```yaml
server:
  ip: 192.168.25.35
  memory: 4096
  cpu: 2
```

# 실행방법
```sh
vagrant up
```

# 삭제
```sh
vagrant destroy --force
```