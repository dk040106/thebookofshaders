# Introduction

<canvas id="custom" class="canvas" data-fragment-url="cmyk-halftone.frag" data-textures="vangogh.jpg" width="700px" height="320px"></canvas>

위 두 그림은 서로 다른 방법을 통해 제작되었습니다. 첫번째 그림은 반 고흐가 직접 페인트를 칠하고, 또 덧칠하는 방식으로 만들어졌습니다. 이 방법은 시간이 꽤 걸렸을 것입니다. 두 번째 그림은 청록색, 붉은색, 노란색, 검은색(CMYK 색 체계: Cyan, Magenta, Yellow, Key plate)의 조합으로 순식간에 제작되었습니다. 두 그림의 가장 큰 차이는, 두 번째 그림은 순서대로 그려지지 않고 모든 부분이 한 번에 그려졌다는 점입니다. 

이 책 *fragment shaders* 는 제목에서부터 알 수 있듯이 Fragment Shader 라는 혁신적인 컴퓨팅 기법에 대한 내용을 담고 있습니다. Fragment Shader는 디지털로 제작되는 이미지들의 차원을 높여주는 기술이며, 마치 그래픽계의 구텐베르크 인쇄술과 같다 할 수 있습니다. 

![Gutenberg's press](gutenpress.jpg)

Fragment shader는 아주 빠른 속도로 화면에 렌더되는 픽셀들을 전부 제어할 수 있도록 해 줍니다. 핸드폰의 필터 기능부터 멋진 3D 비디오 게임들까지 많은 분야에서 사용되는 이유죠. 

![Journey by That Game Company](journey.jpg)

이후 챕터들에서 독자는 Fragment shader가 얼마나 빠르고 강력한지 알 수 있을 것이며, 어떻게 현업과 개인 프로젝트에 적용할 수 있을지 알아갈 것입니다. 

## 누구를 위한 책인가?

====
이 책은 선형대수와 삼각법에 대한 기본적인 이해가 있고, 자신의 작업에서 그래픽 요소들을 개선시키고 싶은 creative coder, 게임 개발자, 그래픽 엔지니어들을 위한 책입니다. (만약 코딩을 처음 해보는 것이라면 다음 링크를 참고하여 코딩에 익숙해진 뒤 이 책으로 돌아오는 것을 추천합니다. [Processing](https://processing.org/))

이 책은 독자들에게 쉐이더를 어떻게 사용하는지부터 프로젝트에 어떻게 적용하는지 가르쳐줄 것이며, 이를 통해 퍼포먼스 향상과 그래픽 퀄리티를 높이는 방법을 보여줄 것입니다. GLSL (OpenGL Shading Language) 쉐이더들은 여러 환경에서 컴파일되고 실행될 수 있기 때문에, 여러분은 여기에서 배운 지식을 OpenGL, OpenGL ES 또는 WebGL을 사용하는 플랫폼에서 적용할 수 있을 것입니다. 다르게 말하면, 여러분들은 여기에서 배운 지식들을 [Processing](https://processing.org/) 각종 스케치, [openFrameworks](http://openframeworks.cc/) 앱, [Cinder](http://libcinder.org/) interactive한 설치형 미술 작품들, [Three.js](http://threejs.org/) 웹사이트들과 iOS/Android 게임들에 적용할 수 있습니다. 

## 이 책은 어떤 내용들을 다루나요?

이 책은 GLSL pixel shader의 사용법에 집중합니다. 우선 쉐이더가 무엇인지 알아볼 것이며, 반복적 모양, 패턴, 텍스처, 애니메이션 등을 만드는 것을 공부할 것입니다. 쉐이딩 언어의 기본에 대해 알고 유용한 곳에 적용해볼 것입니다. 이미지 처리 (이미지 연산, 행렬 합성곱, 블러 효과, 필터, 룩업 테이블(lookup table) 등 및 기타 효과) 와 시뮬레이션 (Conway's game of life, Gray-Scott's reaction-diffusion, 물결 및 물감 효과, Voronoi cells 등) 이 대표적이 예시입니다. 이 책의 막바지에는 Ray Marching에 기반한 고급 기술에 대해서도 알아볼 것입니다. 

*각 챕터별로 직접 실습해 볼 수 있는 예시 작품들이 있습니다.* 작품의 코드를 수정하는 즉시 바뀌는 것을 볼 수 있습니다. 개념들이 추상적이거나 난해할수도 있기 때문에 내용을 이해하기 위해서는 이러한 실습이 꼭 필요할 것이라 생각합니다. 직접 다뤄보는 시간이 많을수록 배우는 속도가 빨라질 것입니다.

이 책이 다루지 않는 부분:

* 이 책은 OpenGL이나 WebGL서적이 *아닙니다*. OpenGL/WebGL은 GLSL이나 fragment shader보다 훨씬 넓고 포괄적입니다. 만약 OpenGL/WebGL에 대해 공부하고 싶다면 다음 자료를 참고하세요. [OpenGL Introduction](https://open.gl/introduction), [the 8th edition of the OpenGL Programming Guide](http://www.amazon.com/OpenGL-Programming-Guide-Official-Learning/dp/0321773039/ref=sr_1_1?s=books&ie=UTF8&qid=1424007417&sr=1-1&keywords=open+gl+programming+guide) (빨간책이라고도 알려져 있습니다) [WebGL: Up and Running](http://www.amazon.com/WebGL-Up-Running-Tony-Parisi/dp/144932357X/ref=sr_1_4?s=books&ie=UTF8&qid=1425147254&sr=1-4&keywords=webgl).

* 이 책은 수학 책이 *아닙니다*. 물론 우리가 다루는 알고리즘과 테크닉들이 선형 대수학과 삼각법을 기본으로 하지만, 수학에 대해서 깊게 다루지는 않을 것입니다. 수학에 관련된 궁금증은 다음 책들을 통해 해결할 수 있을 것이며, 옆에 가져다 놓고 참고하는 것을 추천합니다. [3rd Edition of Mathematics for 3D Game Programming and computer Graphics](http://www.amazon.com/Mathematics-Programming-Computer-Graphics-Third/dp/1435458869/ref=sr_1_1?ie=UTF8&qid=1424007839&sr=8-1&keywords=mathematics+for+games), [2nd Edition of Essential Mathematics for Games and Interactive Applications](http://www.amazon.com/Essential-Mathematics-Games-Interactive-Applications/dp/0123742978/ref=sr_1_1?ie=UTF8&qid=1424007889&sr=8-1&keywords=essentials+mathematics+for+developers).

## 시작하기 위해 무엇을 해야 하나요?

많은 것들이 필요하지 않습니다! WebGL이 지원되는 최신 브라우저 (구글 크롬이나 파이어폭스, 사파리)와 인터넷 연결이 되어 있다면, 페이지 제일 밑에 있는 "Next" 버튼을 누르는 것으로 시작하세요. 

각자 필요에 맞게 다음과 같은 방법으로도 책을 사용할 수 있습니다:

- [오프라인 버전](https://thebookofshaders.com/appendix/)

- [Raspberry Pi에서 브라우저 없이 예제 사용하기](https://thebookofshaders.com/appendix/)

- [프린트용 PDF버전](https://thebookofshaders.com/appendix/)

- [깃허브 레포](https://github.com/patriciogonzalezvivo/thebookofshaders) 에서 이 책의 문제를 고치거나 코드를 공유해주세요. 
