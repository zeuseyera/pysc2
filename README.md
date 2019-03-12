:kr: 스타크래프트 II 학습 환경

| [스타크래프트 II 학습 환경](./README.md) | [환경](./docs/environment.md) | [작은놀이](./docs/mini_games.md) | [지도](./docs/maps.md) |  
| --- | --- | --- | --- |  

| [![fKUyT14G-8](https://img.youtube.com/vi/-fKUyT14G-8/0.jpg)](https://www.youtube.com/watch?v=-fKUyT14G-8) | [![6L448yg0Sm0](https://img.youtube.com/vi/6L448yg0Sm0/0.jpg)](https://www.youtube.com/watch?v=6L448yg0Sm0) | [![WEOzide5XFc](https://img.youtube.com/vi/WEOzide5XFc/0.jpg)](https://www.youtube.com/watch?v=WEOzide5XFc) |  
| --- | --- | --- |  

# 파이스크2 - 스타크래프트 II 학습 환경

[파이스크2(PySC2)](https://github.com/deepmind/pysc2)는 [딥마인드](http://deepmind.com/)의 스타크래프트 II 학습 환경(SC2LE, StarCraft II Learning Environment) 파이썬 부품이다. 이것은 파이썬 강화학습 환경(Python RL Environment)으로 [블리자드 엔터테인먼트(Blizzard Entertainment)](http://blizzard.com/)의 [스타크래프트 II 기계학습 API(StarCraft II Machine Learning API)](https://github.com/Blizzard/s2client-proto)를 제공한다. 이것은 강화학습 연구를 위한 풍부한 환경의 스타크래프트2를 개발하기 위해 딥마인드와 블리자드간 협업하였다. 파이스크2(PySC2)는 스타크래프트2와 상호작용하기 위한 강화학습 똘마니에 대한 인터페이스를 제공한다, 관찰을 얻고 소행을 보내는.

우리는 첨부처럼 [블로그포스트](https://deepmind.com/blog/deepmind-and-blizzard-open-starcraft-ii-ai-research-environment/)와 [논문](https://arxiv.org/abs/1708.04782)을 공개했다, 이것은 깊은강화학습 연구를 위해 스크2 사용를 사용하려는 우리의 동기를 설명한다, 그리고 이 환경을 이용한 일부 기초연구 결과다.

### 요약

면책조항: 이것은 공식 구글제품이 아니다. 
만약 자신의 연구에 스크 II 기계학습 API(StarCraft II Machine Learning API) 와/또는 파이스크2(PySC2)를 사용하는 경우, [스크 II 논문](https://arxiv.org/abs/1708.04782)을 인용하시오.

pysc2@deepmind.com 로 연락하시오.


## 1 빠른 시작 안내

### 1-1) 파이스크2 가져오기

#### 1-1-1) PyPI

파이스크2(PySC2)를 얻는 가장쉬운 방법은 pip를 사용하는 것이다:

``` javascript  
$ pip install pysc2
```

그러면 모든 필수 종속성과 함께 `pysc2`패키지가 설치된다. `virtualenv(가상환경)`은 자신의 종속성 관리에 도움을 줄수 있다. 또한 pip를 향상(upgrade)시킬 필요가 있을수도 있다: `pysc2`설치가 작동하도록 `pip install --upgrade pip`로 향상(upgrade) 하시오. 만약 오래된 시스템에서 실행한다면 `pygame` 종속성을 위해 `libsdl` 라이브러리를 서치해야할 필요가 있을수도 있다.

`pip`는 자신의 `bin` 디렉토리에 바이너리 몇개를 설치할 것이다. `pysc2_play`는 `python -m pysc2.bin.play`의 단축명령으로 사용될수 있다.

#### 1-1-2) Git

아니면 `git`으로 파이스크2(PySC2)를 설치할수 있다. 먼저 파이스크2(PySC2) 저장소를 복제한다, 그런다음 종속성과 `pysc2` 패키지를 설치한다:  

``` javascript  
$ git clone https://github.com/deepmind/pysc2.git
$ pip install pysc2/
```  

### 1-2) 스타크래프트 II 가져오기

파이스크2(PySC2)는 스타크래프트 II 놀이 전체에 의존한다 그리고 API가 포함된 판으로만 작동한다, 이것은 3.16.1 이다 그리고 이 이상.

#### 1-2-1) 리눅스

다음은 리눅스판을 가져오기 위한 블리자드의 [문서](https://github.com/Blizzard/s2client-proto#downloads). 기본적으로, 파이스크2(PySC2)는 이 놀이가 `~/StarCraftII/`에 있을것으로 기대한다. `SC2PATH` 환경변수를 설정 또는 자신만의 실행구성(run_config)을 생성하여 이 경로를 대체할수 있다.

#### 1-2-2) 윈도우/맥

[Battle.net](https://battle.net/)에서 정상적으로 놀이를 설치하라. [시작용(Starter Edition)](https://www.battle.net/download/getInstallerForGame?gameProgram=STARCRAFT_2) 조차도 작동할 것이다. 만약 기본설치 위치를 사용한다면 파이스크2(PySC2)는 나중 바이너리를 찾아야 한다. 만약 설치위치를 변경했다면, 올바른 위치로 `SC2PATH` 환경변수를 설정해야 한다.

파이스크2(PySC2)는 파이썬 2.7+ 또는 3.4+를 실행하는 맥 과 윈도우 시스템에서 작동해야 한다, 그러나 리눅스에서만 완전히 평가되었다. 우리는 다른 시스템과 좋은 호환성을 위해 제안과 패치를 환영한다.

### 1-3) 지도 가져오기

파이스크2(PySC2)는 미리구성된 지도를 많이 가지고 있다. 그러나 놀이를 하기 전에 스크2 `Maps`에 내려받을 필요가 있다.

[승자전(토너먼트, ladder maps) 지도](https://github.com/Blizzard/s2client-proto#downloads)와 [작은놀이(mini games)](https://github.com/deepmind/pysc2/releases/download/v1.2/mini_games.zip)를 내려받는다 그리고 자신의 `StarcraftII/Maps/` 디렉토리로 추출한다.

### 1-4) 똘마니 실행

환경을 평가하기 위해 똘마니를 실행할수 있다. 사용자인터페이스(UI)는 똘마니의 소행을 보여준다 그리고 디버깅과 시각화 목적으로 유용하다.

``` javascript  
$ python -m pysc2.bin.agent --map Simple64
```  

이것은 기본적으로 뿌림하여 똘마니를 실행한다, 그러나 다른것을 지정할수 있다 만약 자신이 원하면.

``` javascript  
$ python -m pysc2.bin.agent --map CollectMineralShards --agent pysc2.agents.scripted_agent.CollectMineralShards
```  

또한 서로 대항하는 두개의 똘마니를 실행할수 있다.

``` javascript  
$ python -m pysc2.bin.agent --map Simple64 --agent2 pysc2.agents.random_agent.RandomAgent
```  

똘마니들의 경주를 지정하기 위해, 상대방의 어려움, 그리고 더, 추가적인 신호(플래그)를 전달할수 있다. `--help`를 사용하여 변경할수 있는 것을 보라.

### 1-5) 사람이 놀이 놀기

디버깅을 위해 주로 사용되는 사람 똘마니 전달기, 그러나 이것은 또한 놀이를 놀기위해 사용된다. 사용자전달기(UI)는 아주 간단하고 불완전하다, 그러나 이것은 놀이의 기본을 이해하면 충분하다. 또한, 이것은 리눅스에서 실행된다.

``` javascript  
$ python -m pysc2.bin.play --map Simple64
```

사용자전달기(UI) 에서, 단축명령 목록을 위해 `?`를 눌러라. 가장 기본적인 것이 있다: 그만하기 위해 `F4`, 다시 시작하기 위해 `F5`, 재생을 저장하기 위해 `F9`, 그리고 놀이 속도를 조절하기 위해 `Pgup`/`Pgdn`. 다른 방법으로는 선택을 위해 마우스를 그리고 왼쪽에 나열된 명령을 하기위해 키보드를 사용한다.

왼쪽은 기본칠 이다. 오른쪽은 똘마니가 받는 특징단이다, 우리에게 유용하게 쓰일 색칠이 되어있다. RGB 또는 특징단 칠을 사용함 또는 사용안함 할수 있다 그리고 해상도는 명령행 플래그를 사용한다.


### 1-6) 재생 관찰

똘마니를 실행하고 사람이 놀기는 기본적으로 재생을 저장한다. 다음을 실행하여 재생을 관찰할수 있다:

``` javascript  
$ python -m pysc2.bin.play --replay <재생하기-위한-경로>
```  

이것은 지도가 놀이로 찾을수 있는한 어떤 재생에 대해서도 작동된다. 놀이를 하는 것 처럼 동일한 제어로 작동한다, 그래서 나오기 위해 `F4`, 속도를 조절하기 위해 `Pgup`/`Pgdn`, 등. `--video` 플래그로 재생 동영상을 저장할수 있다.

### 1-7) 지도 목록

[지도](https://github.com/zeuseyera/pysc2/blob/master/docs/maps.md)를 환경에 알리기 전에 구성할 필요가 있다. 다음 실행으로 알려진 목록을 볼수 있다.

``` javascript  
$ python -m pysc2.bin.map_list
```  

### 1-8) 평가 실행

만약 긁어오기 요청을 제출하기 원한다면, 파이썬 2와 3 모두 통과하는지 평가해 주시오.


## 2 자세한 환경

환경 구성방법 지정의 전체 설명에 대해, 관찰과 소행공간 동작은 [환경 문서](https://github.com/zeuseyera/pysc2/blob/master/docs/environment.md)를 보라.


## 3 작은-놀이 지도

논문에서 참고한 작은-놀이 지도 파일은 `pysc2/maps/`아래에 저장됨 그러나 반드기 `$SC2PATH/Maps`에 설치해야 한다. 위으 내려받기 지침을 따르시오.

지도는 `pysc2/maps/`안에 파이썬 파일로 구성된다. 구성은 놀이꾼과 시간제한을 설정할수 있다, 놀이 결과 또는 과정점수(curriculum score) 사용 여부, 그리고 몇가지 다른 것들. 지도에 관한 더많은 정보에 대해, 그리고 자신만을 위한 구성방법, [지도 문서](https://github.com/zeuseyera/pysc2/blob/master/docs/maps.md)를 봐라.

## 4 재생

재생은 놀이중에 생긴 것을 검토할수 있다. 각 놀이꾼이 논 소행 그리고 관찰을 볼수 있다.

블리자드는 승자전(ladder, tournament)에서 1대1 놀이한 재생을 익명으로 다수를 배포했다. 그 사이트에서 [재생파일](https://github.com/Blizzard/s2client-proto#downloads)을 가져오는 방법에 대한 지침을 찾을수 있다. 또한 자신만의 재생을 검토할수 있다.

재생은 놀이하는 동안 만들어진 관찰과 소행을 얻기위해 재생할수 있다. 관찰은 요청한 해상도로 칠해진 것이다, 그래서 사람이 실제로 본것과 다를수 있다. 마찬가지로 소행은 지점을 지정한ㄷ, 이것은 사람이 화면에서 다른 화소로 반영할 것이다, 그래서 우리의 관찰에 정확히 일치하지 낳을수 있다, 그래고 상당히 비슷할 것이다.

재생은 판(버전)에 의존한다, 따라서 3.16 재생은 3.16.1 또는 3.17 형식(binary)에서 실패한다.

전체놀이를 재생으로 시각화할수 있다, 또는 `pysc2.bin.play`로. 아니면 병렬로 많은 재생을 처리하기 위해 `pysc2.bin.replay_actions`을 실행할수 있다.  



