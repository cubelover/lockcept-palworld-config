# lockcept-palworld-config

> 구성원의 합의로 서버 옵션을 정상화 할 수 있다니, 이 또한 록창섭의 은혜겠지요...

## 워크플로우 및 사용 방법

### 세이브 파일 변환

#### 1. 세이브 파일을 JSON으로 변환 (디코딩)
- `decode.yml` 워크플로우를 실행합니다. 이 과정에서:
  - PalWorldSaveTools가 설치되고, `raw` 폴더의 .sav 파일들이 JSON 형식으로 변환됩니다.
  - 변환된 JSON 파일들은 리포지토리 루트에 저장됩니다 (예: `WorldOption.sav.json`, `LevelMeta.sav.json`, `LocalData.sav.json`).

#### 2. JSON을 세이브 파일로 변환 (인코딩)
- 루트 경로의 JSON 파일을 수정한 후, `encode.yml` 워크플로우를 실행합니다. 이 과정에서:
  - PalWorldSaveTools가 설치되고, 수정된 JSON 파일들이 Palworld 세이브 형식(.sav)으로 변환됩니다.
  - 변환된 .sav 파일은 `raw` 폴더에 저장됩니다.

### 배포 및 재시작

#### 3. Palworld 서버 재시작
- `restart.yml` 워크플로우를 실행하여, Kubernetes 클러스터에서 Palworld 서버 배포를 재시작합니다.

#### 4. Palworld 서버 배포
- `deploy-worldoption.yml` 워크플로우를 실행하여, 서버 설정 파일을 Kubernetes 파드에 복사하고, 배포를 재시작하여 변경사항을 적용합니다.
- `deploy-all,yml` 워크플로우를 실행하여, 전체 설정파일을 덮어쓸 수 있습니다. `Level.sav` 파일이 포함되어 진행사항이 초기화 될 수 있습니다.
