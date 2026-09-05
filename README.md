# Google Colab 클라우드 런타임 연동 및 Pandas 환경 가이드

본 가이드는 구글 코랩(Google Colab)의 고성능 클라우드 컴퓨팅 환경을 연동하여, **Pandas** 등 필수 데이터 분석 라이브러리를 실행할 수 있도록 구성된 패키지입니다.

---

## 📂 파일 구성
- [`colab_runtime_setup.ipynb`](file:///C:/Users/User/.gemini/antigravity/scratch/colab_project/colab_runtime_setup.ipynb): 코랩 클라우드에서 바로 실행할 수 있는 데이터 분석 및 Pandas 검증 노트북
- [`vscode_remote_colab.ipynb`](file:///C:/Users/User/.gemini/antigravity/scratch/colab_project/vscode_remote_colab.ipynb): 로컬 VS Code를 코랩 클라우드 런타임에 직접 터널로 연결하는 설정 노트북
- [`requirements.txt`](file:///C:/Users/User/.gemini/antigravity/scratch/colab_project/requirements.txt): 주요 데이터 분석 & 머신러닝 라이브러리 목록

---

## ⚡ 1. 가장 쉬운 방법: Google Colab 웹에서 바로 실행하기 (추천)

Google Colab은 구글 서버의 클라우드 런타임(리눅스 컨테이너)에서 동작하며, **Pandas, NumPy, Matplotlib, PyTorch 등이 이미 기본 탑재**되어 있습니다.

### 실행 순서:
1. 웹 브라우저에서 [Google Colab](https://colab.research.google.com/)에 접속하고 구글 계정으로 로그인합니다.
2. 상단 메뉴에서 **[파일] > [노트북 업로드]**를 클릭합니다.
3. 생성된 [`colab_runtime_setup.ipynb`](file:///C:/Users/User/.gemini/antigravity/scratch/colab_project/colab_runtime_setup.ipynb) 파일을 선택하여 업로드합니다.
4. 우측 상단의 **[연결(Connect)]** 버튼을 누르면 구글 클라우드 런타임(RAM/디스크 할당)에 자동 연결됩니다.
   - GPU가 필요한 경우: 상단 메뉴 **[런타임] > [런타임 유형 변경] > 하드웨어 가속기 [T4 GPU]** 선택
5. 첫 번째 셀부터 순서대로 `Shift + Enter`를 눌러 실행하면 클라우드 환경에서 Pandas 연산 및 시각화가 즉시 작동합니다.

---

## 💻 2. 로컬 VS Code를 Google Colab 클라우드 런타임에 연동하기

로컬 VS Code의 편한 편집기를 사용하면서 실제 연산(Pandas 및 GPU/CPU)은 구글 코랩 클라우드에서 실행하고자 할 때 사용합니다.

### 실행 순서:
1. Google Colab에 접속하여 새 노트북을 만들거나 [`vscode_remote_colab.ipynb`](file:///C:/Users/User/.gemini/antigravity/scratch/colab_project/vscode_remote_colab.ipynb)를 업로드합니다.
2. 셀을 실행하면 화면에 GitHub 장치 인증 링크(`https://github.com/login/device`)와 8자리 코드가 출력됩니다.
3. 브라우저에서 코드를 입력하여 승인합니다.
4. 로컬 PC의 VS Code에서 **Remote - Tunnels** 확장을 설치한 후, 좌측 하단 초록색 원격 아이콘(`><`)을 눌러 **Connect to Tunnel**을 선택하고 동일 GitHub 계정으로 로그인합니다.
5. 이제 로컬 VS Code에서 코랩 클라우드 파일 시스템과 고성능 파이썬 커널(Pandas 포함)을 그대로 조작할 수 있습니다.

---

## 📦 Pandas 및 추가 라이브러리 관리 팁
- **기본 설치**: 코랩 환경에서는 `import pandas as pd`만 입력해도 즉시 사용 가능합니다.
- **버전 업데이트/추가 설치**: 코드 셀 맨 앞에 느낌표(`!`)를 붙여 실행합니다.
  ```python
  !pip install -U pandas openpyxl
  # 또는
  !pip install -r requirements.txt
  ```
- **구글 드라이브 파일 읽기**:
  ```python
  from google.colab import drive
  drive.mount('/content/drive')
  df = pd.read_csv('/content/drive/MyDrive/my_data.csv')
  ```
