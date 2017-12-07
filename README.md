## Multi-Speaker Tacotron in TensorFlow 사용설명서

#### 소개

Multi-Speaker Tacotron in TensorFlow은 tresorflow를 이용한 딥러닝 음성 합성 시스템입니다. 해당 소프트웨어는 어떤 사람의 목소리를 들려주면 그 사람의 목소리톤뿐만 아니라 발음, 악센트까지 학습하고, 사용자가 원하는 텍스트를 입력하면 그 텍스트를 학습한 목소리로 읽어주는 소프트웨어입니다.

해당 소프트웨어는

Deep Voice 2: Multi-Speaker Neural Text-to-Speech

Listening while Speaking: Speech Chain by Deep Learning

Tacotron: Towards End-to-End Speech Synthesis

해당 논문을 참고해서 만들어졌습니다.

------

#### 선택이유

 제가 이 소프트웨어를 선택한 이유는 이 소프트웨어자체보다는 tresorflow를 이용한 소프트웨어라는데 더 큰 관점을 두고 선택했습니다.앞으로 인공지능의 영역은 더욱 넓어질것이고, 여러 가지 인공지능 소프트웨어가 나올것입니다.

 그러므로 이런 소프트웨어를 사용해봄으로서 tresorflow의 사용법을 익혀보는것도 나쁘지 않다고 생각하여 이 소프트웨어 사용설명서를 작성하게됬습니다.

------

#### 사용방법

사용방법은 크게 4단계로 나눌 수 있습니다. 순서대로 tresorflow 설치하기, 음성데이터 준비하기, 음성 학습시키기, 음성 말들기입니다.

1. TensorFlow 설치

파이썬 설치

<https://www.python.org/downloads/release/python-363/>

파이썬 설치 주소입니다.

[파이썬]: https://cdn.discordapp.com/attachments/388424141927219211/388424181366390814/image2.png	"파이썬 다운로드"



아나콘다 설치

<https://www.anaconda.com/download/>1

아나콘다 설치 주소입니다.

[아나콘다]: https://cdn.discordapp.com/attachments/388424141927219211/388424190199595011/image1.png	"아나콘다 다운로드"



TensorFlow 설치

Anaconda Prompt를 실행합니다.

다음 명령어를 순서대로 입력합니다.

```
1> python –m pip install —upgrade pip
2> conda create –n tensorflow python=3.5
2.1> y/n에서 y
3> activate tensorflow
4> pip install tensorflow
```



필수라이브러리 설치

<https://github.com/GSByeon/multi-speaker-tacotron-tensorflow.git>

에서 zip파일을 다운로드 받고 압출을 풀어준다.

그다음 cmd에서 cd명령어를 이용해 해당 폴더 위치로 이동한다.

[cmd]: https://cdn.discordapp.com/attachments/388424141927219211/388425052611149824/image3.png	"예시"

다음명령어를 입력해 필수라이브러리로 이동한다

```
pip3 install -r requirements.txt
python -c "import nltk; nltk.download('punkt')"
```

​     

2. 학습할 데이터 준비하기

datasets\chosun 경로에

audio폴더와 alignment.json를 구성합니다.

audio폴더 내부에 mp3파일을 추가합니다.

001.mp3, 002.mp3, 003.mp3...

```
alignment.json

{
    "./datasets/chosun/audio/001.mp3": "광주광역시 동구 서남동",
    "./datasets/chosun/audio/002.mp3": "조선대학교입니다",
    "./datasets/chosun/audio/003.mp3": "음성학습을 실행합니다",
}
```

다음 명령어를 통해 학습데이터를 준비합니다.

```
python3 -m datasets.synthesizer_data ./datasets/chosun/alignment.json
```

​     

3. 학습하기

다음 명령어를 실행합니다.

```
python3 train.py —data_path=datasets/chosun
```

다시 학습할 때 명령어입니다.

```
python3 train.py --data_path=datasets/chosun —load_path logs/chosun-20171208
```

​     

4. 음성 만들기

다음 명령어를 실행합니다.

```
python3 synthesizer.py --load_path logs/chosun-20171208 —text "마이크테스트 하나 둘 셋"
```

명령어를 실행하면 "마이크 하나 둘 셋"을 학습한 음성으로 말합니다.