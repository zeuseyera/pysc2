
| [스타크래프트 II 학습 환경](../README.md) | [환경](../docs/environment.md) | [작은놀이](../docs/mini_games.md) | [지도](../docs/maps.md) |  
| --- | --- | --- | --- |  

# 환경

**알맹이**

1. 스타크래프트 II

- [스타크래프트 II는 무엇인가?](#스타크래프트-II란)
- 판
- 놀이와 소행 속도
  - 놀이 속도
  - APM 계산
  - APM 과 공정성
- 결정과 뿌림

2. 소행과 관찰

2-1) [관찰](#관찰)

- 공간/시각
  - RGB 화소
  - 특징단
  - 작은지도
  - 화면
- 구조
  - 일반 놀이꾼 정보
  - 제어 무리
  - 단일 선택
  - 다중 선택
  - 화물
  - 구축 기다림
  - 가능 소행
  - 지난 소행
  - 소행 결과
  - 알리미

2-2) [소행](#소행)

- 소행 목록
- 소행 부류
- 일반 대 특정 소행
- 사용 본보기

3. 강화학습 환경

- 환경 싸개

4. 똘마니


---

## 1 스타크래프트 II

<a name="스타크래프트-II란"></a>
### 1-1) 스타크래프트 II는 무엇인가?

[스타크래프트 II](https://en.wikipedia.org/wiki/StarCraft_II:_Legacy_of_the_Void)는 [블리자드](http://blizzard.com/)가 작성한 [실시간전략(RTS, Real Time Strategy)](https://en.wikipedia.org/wiki/Real-time_strategy) 놀이다. 이것은 [스타크래프트 피의전쟁(Broodwar)](https://en.wikipedia.org/wiki/StarCraft:_Brood_War)을 계승한 것이다. 이것은 가장 성공적인 실시간전략놀이중 하나다. 스타크래프트 II는 수백만명이 놀고있다, 그리고 프로 연맹(league)이 있다. [스타크래프트에서 목표](http://us.battle.net/sc2/en/game/guide/whats-sc2)는 기지구축, 경제관리, 군대구축, 그리고 자신의 적을 파괴하는 것이다. 제3자 관점에서 자신의 기지와 군대를 제어한다, 그런 다음 최대 효과를 위해 자신의 집단을 다중-작업과 미세-관리를 한다. 스타크래프트는 3가지 별개의 종족이 있다: [테란](https://www.youtube.com/watch?v=Fmu8PsUDDtQ), [프로토스](https://www.youtube.com/watch?v=m0g0MpllFCs) 그리고 [저그](https://www.youtube.com/watch?v=Lq74R7wWAnQ), 이것은 다른 집단과 전략을 가진다.

놀이는 혼자놀기 홍보가 있다, 그렇지만 대부분의 사람들은 [배틀넷(Battle.net)](https://starcraft2.com/ko-kr)에서 여럿이 논다. 이것은 내장된 봇이 있다, 그러나 상당히 약하고 예측할수 있다, 그리고 더 강한 속임수(cheat)를 쓸수있다.

이 스타크래프트를 배우기 위한 온라인 자원이 많이 있다, [배틀넷](https://starcraft2.com/ko-kr) 포함, [리퀴피디아](http://liquipedia.net/starcraft2/StarCraft)와 [위키아](http://starcraft.wikia.com/). 지도를 만들기 위해 [SC2Mapster](https://sc2mapster.gamepedia.com/SC2Mapster_Wiki)를 확인하라.

### 1-2) 판

블리자드는 정기적으로 스타크래프트 II를 갱신한다. 이러한 갱신은 대략 매달 한다, 새로운 특징을 도입할수 있다, 그리고 종족을 더 균형있게 만들기 위해 자주 사소한 놀이와 균형을 변경한다. 재생은 생성된 특정 판에 구속된다.

### 1-3) 놀이와 소행 속도

실시간전략 놀이의 늼는 놀이가 실시간으로 실행되는 것이다. 그러나 실제로는, 시뮬레이션은 초당 16 ~ 22회 갱신된다, 자신의 [놀이 속도](http://wiki.teamliquid.net/starcraft2/Game_Speed)에 따라, 그리고 모든 중간에 칠해진 장면은 그냥 덧붙임된 것이다.

#### 1-3-1) 놀이 속도

API를 통해 주기를 제어할수 있는 소행을 한다. 초당 16 ~ 22 단계에서 실행하는 대신에, 자신이 원하는 만큼 빠름 또는 느림 단계를, 자신이 원하면. 만약 똘마니가 능력이 있다면 실시간보다 훨씬 빠르게 실행할수 있게 허용한다, 또는 만약 똘마니를 때때로 벼림에 약간의 시간을 할애하기 위해 잠시멈춤할 필요가 있다면 훨씬 느리게. 이것은 또한 어떤 지연도 결코 없다는 것을 의미한다. 최대속도는 step_mul/render 주기에 의존한다, 그리고 complexity/unit 장면 수. 실시간의 10배는 드물지 않다 그리고 간단한 지도에 대해 훨씬 높을수 있다.

#### 1-3-2) APM 계산

놀이는 분명하지 않은 방법으로 APM을 계산하고 보고한다. 이것은 가장자리 말기로 카메라 움직임 소행을 계수하는 방법이 분명하지 않다, 또는 얼마나 많은 소행이 건물을 구축하는지. 여기에 놀이에 의해 실제로 계수되는 방법의 규칙이 있다.

이것은 놀이에 의해 실제로 보고되는 두개의 유형이 있다:

- 분당 소행(APM, Actions Per Minute): 모든 소행 계수.
- 효과적인 분당 소행(EPM, Effective Actions Per Minute): 아무런 효과가 없는 소행은 걸러낸다(예: 중복 선택).

다른 소행은 소행의 다른 번호로 계수한다:

- 대상이 있는 명령 = 2 (예: 이동, 공격, 건물 구축)
- 대상이 없는 명령 = 1 (예: 정지, 집단 벼림, 화물 내림)
- 잽쌈(Smart) = 1 (오른쪽 클릭)
- 무리의 선택과 제어 = 1
- 그밖의 모든것 = 0 (예: 카메라 움직임)

#### 1-3-3) APM 과 공정성

사람은 장면당 하나의 소행을 할수 없다. 사람의 범위는 30-500 분당 소행(APM)이다, 초보자는 30, 평균은 60 ~ 100, 그리고 전문가는 200 이상(초당 3회 이상!). 이것은 빠른 봇이 가능한 것에 비해 사소한 것이다. [BWAPI](http://bwapi.github.io/)는 개별적으로 부대를 제어한다 그리고 일상적으로 5,000 APM 이상을 달성한 것은 사람에 대해 분명히 불가능하다 그리고 [불공평](https://youtu.be/IKVFZ28ybQs?t=45s)하거나 심지어 [짓밟힌](https://youtu.be/0EYH-csTttw?t=28s) 것으로 간주된다. 부대를 개별적으로 제어하지 않아도 높은 정밀도로 훨씬 빨리 소행할수 있다는 것은 불공평한 것이다.

적어도 공평하게 놀기 위해서는 APM을 인위적으로 제한하는 것이 좋은 생각이다. 쉬운 방법은 똘마니가 얼마나 자주 관찰을 얻고 소행을 취할수 있는지를 제한하는 것이다, 그리고 관찰당 한번의 소행으로 제한하라. 예를 들어 모든 **_N 번째_** 관찰만 취함으로써 이것을 할수 있다, 여기에서 **_N_** 은 논쟁의 여지가 있다. `20`의 값은 분당 소행(APM)이 대략 50과 같다 그런데 `5`는 분당 소행(APM) 대략 200이다, 그래서 그것은 놀기위한 합리적인 범위다. 더욱 정교한 방법은 똘마니의 모든 관찰을 주는 것이다 그러나 실제로 영향을 미치는 소행의 수를 제한한다, 소행으로 계수(간주)되지 않는 **소행안함(no-ops)** 을 주로 **만들도록 강제** 한다.

아마도 모든 소행을 동등한 것으로 생각하는 것이 좋다, 카메라 움직임 포함, 아주빠른 카메라 움직임을 허용하면 똘마니가 속일수 있기 때문이다.

### 1-4) 결정과 뿌림

스타크래프트 II는 대부분 결정론적이다, 그러나 이것은 허울뿐인 이유에 대해 주로 뿌림성이 있다. 두개의 주요 뿌림 요소는 무기속도와 갱신주문이다.

무기의 뿌림성은 부대(unit)가 발사후 다음쏘기를 얼마나 빨리 얻을수 있는지가 본질이다 그리고 거의 모든 부대(unit)에 대해서 -1 ~ 2 사이의 놀이단계다. 이 구상은 해병 한 무리 모두가 함께 발사시작할수 있다는 것이다, 그러나 다음 쏘기를 위한 작은 뿌림 `+/-`는 무리를 덜 로봇스럽에 만들 것이다 그리고 영원히 동기된 발사를 막는다. 이것은 또한 공정한 대결(예: 1 대 1 해병)인 뿌림 결과를 가져올 것이다.

갱신 요구는 뿌려진 것이다 그리고 주어진 놀이 도돌이에서 벌어짐(event)요구를 결정한다. 예를 들어, 만약 같은 놀이 도돌이에서 서로에 대한 되먹임을 던지는 두개의 고위기사(High Templar)를 가지고 있다면, 이것은 어느 하나가 먼저 피해를 입히고 승리하는 것은 뿌림일 것이다.

부대 자동-표적은 결정적이다, 하지만 복잡하다. 이것은 무기의 훑음 거리, 위협 그리고 지원을 기반으로 한다. 부대는 무기가 있는 적을 없는것 보다 높은 위협으로 간주할 것이다, 그리고 대응사격을 할수있는 적들이 높은 우선권이 주어질 것이다 대응사격을 할수 없는 것보다. 대응사격을 할수 없는 부대(예: 미사일 회전탑과 해병) 그러나 거것이 연합된 부대(예 수송용, medivac)를 공격하면 도움요청을 유발하고 우선권이 증가한다. 치료자는 치유할때 우선권이 증가한다. 만약 두개의 대상이 같은 우선권이면 더 가까운것이 선택될 것이다.

이러한 뿌림 자원은 뿌림씨앗을 설정하여 제거/완화 할수 있다. 재생은 뿌린 씨앗을 포함하는 놀이 설정을 저장한 것으로 작업한다, 모든 놀이꾼의 소행목록뿐만 아니라, 그런 다음 시뮬에이션을 재생한다.

## 2 소행과 관찰

스타크래프트 II는 매우 풍부한 소행과 관찰공간을 가지고 있다. 놀이는 공간(시각) 과 구조요소 모두 출력한다. 구조요소는 문자와 숫자가 많아서 똘마니가 읽기를 배우는것을 기재하지 않기 때문에 제공된다, 특히 낮은 해상도에서. 이것은 또한 사람이 본것과 정확히 같은 시각으로 재생을 되돌리는 것은 어렵기 때문이다.

**중요한 알림:**

공간 관찰은 `(y, x)`처럼 y-주화면 좌표공간에 있다. 소행은 화면 또는 작은지도의 지점(한점)이 요구된다, 그러나 좌표는 `(y, x)`로 기대한다. 원점 `(0, 0)`은 두 경우 좌-상 모서리다.

화면 좌표를 소행으로 전달하는 본보기에 대한 [짜여진 똘마니](https://github.com/zeuseyera/pysc2/blob/master/pysc2/agents/scripted_agent.py)를 보라:

``` javascript
# 공간 관찰은 먼저 y-coordinate 를 가진다:
y, x = (obs.observation["feature_screen"][_PLAYER_RELATIVE] == _PLAYER_NEUTRAL).nonzero()

# 소행은 먼저 x-coordinate 를 기대한다:
target = [int(x.mean()), int(y.mean())]
action = actions.FunctionCall.Move_screen("now", target)
```

<a name="관찰"></a>
### 2-1) 관찰

#### 2-1-1) 공간/시각

**- RGB 화소**

RGB 화소는 주화면 영역 뿐만 아니라 작은 지도도 자신이 선택한 해상도로 할수 있다. 이것은 사람이 보는것 처럼 같은 원근법 카메라를 사용한다, 그러나 명령카드 처럼 모든 화면 주변의 보태진 회색(테두리)은 포함하지 않는다, 선택상자, 구축기다림, 등. 이것들은 `rgb_screen`과 `rgb_minimap` 처럼 보여준다.

**- 특징단**

놀이는 또한 특징단을 보여준다. 이것들은 정보가 분해되고 구조화된 점을 제외하고 RGB 화소로 같은 정보를 표현한다. 이것은 화면과 작은지도 사이에 세분화된 ~ 25개의 특징단이 있다 그리고 `feature_screen`과 `feature_minimap`로 보여준다.

전체 목록은 `pysc2.lib.features`에 정의되어 있다.

**- 작은지도(Minimap)**

작은지도는 지도전체의 낮은해상도로 보기이다. 이것은 진행되는 모든것의 대충보기를 제공한다, 그러나 화면보다 자세하지 않다.

작은지도의 해상도를 지정할수 있다. 지도 범위는 32 ~ 256<sup>2</sup>이다, 100 ~ 256<sup>2</sup> 범위로 일반적인 사람용 지도를 포함한다. 1080p에서 노는 사람은 화면 좌하단 모서리에서 ~ 250<sup>2</sup>의 해상도를 얻는다.

이것들은 작은지도 특징단이다:

- height_map: 지형 높이(표고)를 보여준다.  
- visibility: 지도의 어떤 부분은 숨겨져 있다, 이미 보았거나 현재 볼수 있다.  
- creep: 저그의 크립이 있는 부분.  
- camera: 지도의 어떤 부분이 화면단에서 보이는 것이다.
- player_id: 자신의 부대, 절대 고유번호(ID).
- player_relative: 어떤 부대가 우호적 대 적대적인가 이다. [0, 4]에서 값을 취한다, 부대 각각은 [배경(background), 자신(self), 동맹(ally), 중립(neutral), 적(enemy)]를 의미한다.
- selected: 선택된 부대.

**- 화면(Screen)**

화면은 지도 일부를 높은해상도로 보기이다.

이것은 위아래 직각 카메라로 칠해진 것이다, 사람의 실제 놀이에서 얻을수 있는 원근감있는 카메라와는 대조적이다. 이것은 어떤 시각은 어렵게 만든다(예: 크기로 높이(표고)를 볼수 없다), 그러나 이것은 또한 다른것들은 쉽게 만든다(예: 단위는 카메라의 움직임에 따라 크기가 변경되지 않는다). 이것은 또한 보이는 영역이 지도의 직사각형 일부임을 의미한다, 실제 놀이의 사다리 모양과는 대조적이다. 이것은 사람은 볼수 없고 똘마니는 볼수 있는 비트로 된 지도를 의미한다, 그리고 반대의 경우, 그러나 이것은 대체로 비슷하다.

작은 단위는(예: 해병 또는 저글링) 놀이단위가 `~0.75`다. 카메라는 놀이단위 너비가 24 다. 만약 32<sup>2</sup>의 화면 해상도를 지정하면, 이것은 1 화소 너비 단위를 의미한다, 이 위치의 정밀도는 아주 낮다는 것을 의미한다. 만약 큰 무리가 있다면 얼마나 많이 있는지 말할수 없을 것이다. 적어도 64<sup>2</sup>의 해상도를 놀이로 권장한다.

이것들은 화면 특징단이다:

- height_map: 지형 높이(표고)를 보여준다.  
- visibility: 지도의 어떤 부분은 숨겨져 있다, 이미 보았거나 현재 볼수 있다.  
- creep: 저그의 크립이 있는 부분.  
- camera: 지도의 어떤 부분이 화면단에서 보이는 것이다.
- player_id: 자신의 부대, 절대 고유번호(ID).
- player_relative: 어떤 부대가 우호적 대 적대적인가 이다. [0, 4]에서 값을 취한다, 부대 각각은 [배경(background), 자신(self), 동맹(ally), 중립(neutral), 적(enemy)]를 의미한다.
- unit_type: 부대 고유번호(ID), `pysc2/lib/units.py`에서 찾아볼수 있다.
- selected: 선택된 부대.
- hit_points: 부대가 가진 찍은 지점 수.
- energy: 부대가 가진 에너지 량.
- shields: 부대가 가진 방어 량. 프로토스 부대만.
- unit_density: 이 화소에 있는 부대의 량(부대 밀도).
- unit_density_aa: `anti-aliased`판의 `unit_density`는 화소당 16이다. 이것은 보조화소로 부대 위치와 크기를 제공한다. 예를 들어 만약 부대가 정확히 1화소 직경이면, `unit_density`는 실제중심 화소가 어디에 있는지에 관계없이 정확히 1 화소로 보여준다, `unit_density_aa`는 각 화소가 부대로 덮여진 량. 하나의 부대는 한 화소보다 작다 그리고 화소에서 중심은 최대값보다 작은 값을 제공한다. 한 화소의 모서리 근처에 중심을 둔 직경 1인 하나의 부대는 덮인 4개의 화소 각각에 그 값의 대략 1/4을 제공한다. 만약 여러 부대가 하나의 화소를 덮는다면 덮여있는 화소의 비율은 합산된다, 최대 256 까지

#### 2-1-2) 구조

놀이는 똘마니가 화소로부터 읽지 않을 것으로 예상되는 상당한 양의 구조화된 자료를 제공한다. 대신에 의미 그대로의 의미인 텐서로 주어진다.

**- 일반 놀이꾼 정보**

`(11)`는 일반정보를 보여주는 텐서(11x1 배열-11개의 속성).

- 놀이꾼_고유번호(player_id)
- 광물(minerals)
- 베스핀(vespene)
- food used (otherwise known as supply)
- food cap
- food used by army
- food used by workers
- 땡땡이 일꾼 수(idle worker count)
- 군대 수(army count)
- 공간이동 통문 수(warp gate count (for protoss))
- 애벌레 수(larva count (for zerg))

<a name="제어-무리"></a>
**- 제어 무리(Control groups)**

`(10, 2)`는 10개 제어무리(단위 유형과 수) 각각에 대해 보여주는 텐서(10x2 배열). 이 텐서에서 찾기참조(index)는 `control-group` 소행에 의해 참조된다.

[제어 무리(Control groups)](http://learningsc2.com/tag/control-groups/)는 선택집합을 기억하는 방법이다 그래서 나중에 쉽게 다시부름 할수있다.

**- 단일 선택(Single Select)**

`(7)`는 선택된 부대에 관한 정보를 보여주는 텐서(7x1 배열).

- 부대 유형(unit type)
- 놀이꾼 관계(player_relative)
- 생명력(health)
- 보호막(shields)
- 에너지(energy)
- 취한 수송수단(수송선 안에 있다면, transport slot taken if it's in a transport)
- 구축 징행 백분율(아직 구축중 이라면, build progress as a percentage if it's still being built)

**- 다중 선택(Multi Select)**

`(n, 7)`는 단일 선택과 같은 텐서다 그러나 `n`개 모두 선택한 단위에 대해. 이 텐서에서 찾기참조(index)는 `select_unit` 소행에 의해 참조된다.

**- 화물(Cargo)**

`(n, 7)`는 단일 선택과 비슷한 텐서다, 그러나 수송선 안에 있는 모든 부대에 대해. 이 텐서에서 찾기참조(index)는 `unload` 소행에 의해 참조된다.

**- 구축 기다림(Build Queue)**

`(n, 7)`는 단일 선택과 비슷한 텐서다, 그러나 건물 생산에 의해 구축되는 모든 부대에 대해. 이 텐서에서 찾기참조(index)는 `build_queue` 소행에 의해 참조된다.

**- 가능 소행(Available Actions)**

`(n)`는 관찰 시에 가능한 소행 고유번호 모두를 나열한 텐서.

**- 지난 소행(Last Actions)**

`(n)`는 마지막 관찰 이후 성공적으로 수행된 소행 고유번호 모두를 나열한 텐서. 시도했지만 실패한 소행은 여기에 포함되지 않는다.

**- 소행 결과(Action Result)**

`(n)`는 소행 결과를 주는 텐서(대개 크기는 1).

**- 알리미(Alerts)**

`(n)`는 자신이 주요 방법으로 공격을 받았을때에 대한 텐서(대개 비어있음, 때때로 크기는 1, 최대 2).

<a name="소행"></a>
### 2-2) 소행

스크2(SC2) 소행공간은 아주 크다. 수백가지의 가능한 소행이 있다, 어떤 화면 또는 작은지도 공간에서 취할수 있는 지점이 많다, 그리고 추가적인 수정기로 취하는 것이 많다. 만약 소행공간을 1차원으로 펼치면(나누면), 가는 소행은 수백만 또는 수십억개를 가질 것이다, 이것들 대부분은 유효하지 않다, 그리고 이것들의 수많은 것은 연관성이 높다. 따라서 소행공간을 분리하여 펼치는 것은 매우 적합하지 않다.

대신에, 구성결합(소행의)을 주기에 충분히 풍부한 소행함수를 생성했다, 고유계층 복잡성없이. 이것은 특정 유형의 인수를 취할수 있는 C-풍 함수 모형의 정신을 기반으로한다. 유효한 유형과 함수의 전체 집합은 `pysc2.lib.actions`에서 `ValidActions`에 정의되었다, 그런 다음 각 관찰은 가은한 함수가 이 프레임에서 유효한지 여부를 지정한다. 각 소행은 `pysc2.lib.actions`에서 모든 고유값(argument)이 채워진 하나의 `FunctionCall`이다.

유형과 함수의 전체 집합은 `pysc2.lib.actions`에 정의되었다. 함수집합은 직접작성했다 그리고 사람이 취한 소행으로만 제한한다, 수많은 재생 수에 의해 볼수 있는 것 처럼. 함수를 직접작성했다는 것은 사용자지도(custom map)에 생성된 소행은 `pysc2.lib.actions`에 추가될 때까지 사용할수 없다는 것을 의미한다.

이러한 소행이 뜻하는 의미는 주로 다음을 검색하여 찾을수 있다: `liquipedia.net/starcraft2` 또는 `starcraft.wikia`.

**- 소행 목록**

존재하는 실행 소행을 보기 위해:

``` javascript
$ python -m pysc2.bin.valid_actions
```

선택지정을 함께 `--hide_specific`, `--screen_resolution` 또는 `--minimap_resolution` 만약 정확한 값에 관하여 관심이 있다명. 이것은 일부 비슷한 것을 출력한다:

``` javascript
   0/no_op                       ()
   1/move_camera                 (1/minimap [64, 64])
   2/select_point                (6/select_point_act [4]; 0/screen [84, 84])
   3/select_rect                 (7/select_add [2]; 0/screen [84, 84]; 2/screen2 [84, 84])
   4/select_control_group        (4/control_group_act [5]; 5/control_group_id [10])
   5/select_unit                 (8/select_unit_act [4]; 9/select_unit_id [500])
   6/select_idle_worker          (10/select_worker [4])
   7/select_army                 (7/select_add [2])
   8/select_warp_gates           (7/select_add [2])
   9/select_larva                ()
  10/unload                      (12/unload_id [500])
  11/build_queue                 (11/build_queue_id [10])
  12/Attack_screen               (3/queued [2]; 0/screen [84, 84])
  13/Attack_minimap              (3/queued [2]; 1/minimap [64, 64])
  14/Attack_Attack_screen        (3/queued [2]; 0/screen [84, 84])
  19/Scan_Move_screen            (3/queued [2]; 0/screen [84, 84])
  23/Behavior_CloakOff_quick     (3/queued [2])
  26/Behavior_CloakOn_quick      (3/queued [2])
  42/Build_Barracks_screen       (3/queued [2]; 0/screen [84, 84])
  44/Build_CommandCenter_screen  (3/queued [2]; 0/screen [84, 84])
 220/Effect_Repair_screen        (3/queued [2]; 0/screen [84, 84])
 221/Effect_Repair_autocast      ()
 264/Harvest_Gather_screen       (3/queued [2]; 0/screen [84, 84])
 303/Morph_Lair_quick            (3/queued [2])
 317/Morph_SiegeMode_quick       (3/queued [2])
 322/Morph_Unsiege_quick         (3/queued [2])
 331/Move_screen                 (3/queued [2]; 0/screen [84, 84])
 333/Patrol_screen               (3/queued [2]; 0/screen [84, 84])
 405/Research_Stimpack_quick     (3/queued [2])
 451/Smart_screen                (3/queued [2]; 0/screen [84, 84])
 452/Smart_minimap               (3/queued [2]; 1/minimap [64, 64])
 453/Stop_quick                  (3/queued [2])
 477/Train_Marine_quick          (3/queued [2])
           *** 100s more lines ***
```

이것은 다음처럼 읽어야 한다: `<함수고유번호>/<함수이름>(<유형 고유번호>/<유형 이름> [<값 크기>, *]; *)`. 

일부 본보기:

- `1/move_camera (1/minimap [64, 64])`은 `move_camera`(고유번호 `1`)함수다, 이것은 `minimap`(고유번호 `1`)이라는 이름의 하나의 고유값을 취한다, 이것은 `[0, 64]`범위 각각에 작은지도의 좌표를 표현하는 두개의 정수가 필요하다.
- `331/Move_screen (3/queued [2]; 0/screen [84, 84])`은 `Move_screen`함수(고유번호 `331`)다, 이것은 두개의 고유값을 취한다: `queued`(고유번호 `3`)는 부울이다 그리고 이 소행이 지금 또는 이전소행 후에 일어나야 하는지 여부를 나타낸다, 그리고 `screen`(고유번호 `0`)은 `[0, 84]`범위 각각에 화면에서 화소를 표현하는 두개의 정수를 취한다.

함수 이름은 고유하고, 안정적이고 읨가 있어야 한다. 함수와 고유번호는 함수(`function`)와 유형(`type`) 목록에 대한 찾기참조(index)다.

유형(`type`)은 함수 호출에서 사용할수 있는 미리정의된 유형고유값 목록이다. 정확한 정의는 `pysc2.lib.actions.TYPES`에 있다.

**- 소행 부류(Action categories)**

변형(`Morph`) 소행은 낱개(unit)를 다른 낱개(unit)로 변환한다, 관찰에서 적어도 `unit_type`에 따라. 예를들어 `Morph_Lair_quick`는 부화장(`hatchery`)을 은신처(`lair`)로 변형(`Morph`)한다; `Morph_SiegeMode_quick`와 `Morph_Unsiege_quick`는 포위탱크를 탱크와 포위(공성, `siege`) 사이의 방식으로 변형(`Morph`)한다. 효과(`Effect`)는 한가지 효과다, 드물게 취소할수 있다. 행동(`Behavior`)은 켜고 끌수 있다 그러나 낱개(unit)의 유형을 변경할수 없다.

**- 일반 대 특정 소행(General vs Specific actions)**

스타크래프트 II는 능력에 관하여 말한다. 때때로 하나의 개념은 많은 낱개(unit)는 하나의 능력으로 구현할수 있다(예: 이동, 고정, 순찰), 그리고 때때로 많은 능력(예: 공격, 파고들기, 취소, 이륙/착륙). 파고들기(`Burrow`)는 간단한 본보기다 여기서 각 저그 부대는 파고들수 있는 자신의 능력이 있다(`BurrowDown_Drone`, `BurrowDown_Zergling`, 등). 이런 것들을 개별적으로 노출시키면 소행공간은 한층 더 복잡하게 만들 것이다, 그리고 [APM 제한](https://github.com/zeuseyera/pysc2/blob/master/docs/environment.md#apm-and-fairness)이 주어지면 한번에 군대 전체가 파고들기 어렵게 만든다, 그래서 우리는 놀이 UI에서 함께 일어나거나 같은 키를 사용할수 있는 특별한 능력 모두를 합하여 일반능력 개념을 추가했다. 만약 특정 능력이 주어지면(예: `BurrowDown_Zergling`) 이것은 그 능력을 지원하는 특정 낱개(unit)만 영향을 미친다(예: 저글링), 반면에 해당하는 일반능력(파고들기`BurrowDown`)이 주어지면 이것은 지원하는 모든 낱개(unit)에 영향을 줄 것이다.

공격은 이 경우는 명확하지 않은 것이다. 이것에는 공격(`Attack`)이 있다, 이것은 UI가 하는 것에 해당하는 일반 능력이다, 그러나 공격 낱개(unit)에 대해 실제 공격공격(`Attack_Attack`) 실행은 가려진 것이다, 공격할수 없는 수송서(medivac) 같은 지원 낱개(unit)에 대해 조사이동(`Scan_Move`)을 한다 그러나 그들이 할수 있는 것처럼 따라와야 한다, 방어건물에 대해 건물공격(`Attack_AttackBuilding`)(예: 미사일 회전탑) 그리고 탑재된 낱개(unit)를 공격하기 위해 벙커에 대해 공격재지정(`Attack_Redirect`).

지금은 일반소행만 환경 api를 통해 노출된다 그래서 일반소행만 가능한 소행 관찰만 반환되어야 한다.

`pysc2.lib.actions.FUNCTIONS`에서 특정 함수는 일반참여를 참조하는 추가적인 참여를 가진다.

**- 사용 본보기**

`ValidActions`을 소멸시키고 `FunctionCall`을 채우는 방법 본보기에 대한 뿌림 똘마니를 살펴보라.

다음 조각은 사람이-읽을수 있는 가능소행 목록을 인쇄하는 방법을 보여준다:

``` javascript
# pysc2/lib 폴더에서 actions 모듈을 탑재한다
from pysc2.lib import actions

for action in obs.observation.available_actions:
    print(actions.FUNCTIONS[action])
```

## 3 강화학습 환경

스크2(SC2) 주요 환경은 `pysc2.env.sc2_env`에 있다, 더불어 소행과 관찰 공간은 `pysc2.lib.features`에 정의되어 있다.

가장 중요한 고정값은 `map_name`이다, 이것은 지도를 찾는 방법이다. `pysc2.bin.map_list`를 사용 아니면 `pysc2/maps/*.py`에서 주시하여 이름을 찾는다.

놀이꾼(`players`)은 자신이 놀이꾼 수와 유형을 지정하게 한다. 지금은 혼자만 또는 놀이꾼 둘을 지원한다. `sc2_env.Agent`또는`sc2_env.Bot` 개체목록을 제공, 겨루기와 난이도를 지정한다. 똘마니 두개를 지정하면 그들간 통신하는 스크2 두개의 대리자(instance)가 시작될 것이다, 그리고 메모리와 CPU는 놀이꾼 혼자 노는것의 두배를 소모한다.

`agent_interface_format`는 자신이 각 똘마니가 사용할 관찰과 소행 전달기를 지정하게 한다. `feature_dimensions`와 `rgb_dimensions`는 자신이 공간 관찰 해상도를 지정하게 한다. 높은 해상도가 명백하게 제공하는 것은 높은 위치정밀도, 큰 관찰비용 뿐만아니라 큰 소행공간, 그리고 칠하는 시간이 느려진다.

만약 특징과 rgb 관찰 양쪽에 대해 교구한다면 자신이 사용할 소행공간을 지정해야 한다. 이것은 자신이 다른것에서 배우는 동안 하나의 소행을 하도록 한다.

`step_mul`는 자신이 관찰과 소행을 건너뛰게 한다. 예를 들어 16의 `step_mul`은 환경은 똘마니가 소행하는 사이에 16순간이 나아간 걸음을 가져오는 것을 의미한다(16 보 = 1의 놀이순간). 이것은 이러한 장면에서 일정한 관찰은 무시하고 소행은 보내지 않는 것과 같은 것이다, 제외한 이것은 또한 건너뛴 장면을 칠할 필요가 없기 때문에 환경이 가속된다.

`save_replay_episodes`와 `replay_dir`는 재생저장 빈도와 저장위치를 지정한다.

자신의 똘마니가 환경과 더불어 상호작용하도록 하기위해 `run_loop.py`를 사용한다.

**- 환경 싸개(Environment wrappers)**

여기에 미리-만든 환경싸개 하나가 있다:

- `available_actions_printer`: 각각의 가능한 소행을 보이는 대로 인쇄한다.

## 4 똘마니

여기에 기본 똘마니 한쌍이 있다.

- `random_agent`: 그냥 뿌림으로 논다, 유효한 이동을 만드는 방법을 보여준다.
- `scripted_agent`: 이것은 하나의 작은 놀이에 대해 짜여진 것이다.

