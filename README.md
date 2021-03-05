# Project Title / 42seoul_cube3d_miniLibx 사용법

## contents  

1. 소개


## 소개

42seoul subject 중 cube_3d라는 과제가 있으며 이 과제를 수행하기 위해서는 miniLibx 사용법을 알아야하며 
miniLibx가 제공하는 함수들의 사용법을 알아야지 cube_3d를 하나하나 만듬에 있어서 로직 구조를 어떻게 해야할지 설계를 할 수 있다.
그럼으로 제공하는 함수에 대해 자세히 정리해보고자 따로 사용법에 대해서 설명하려한다.


## 시작함수

mimiLibx 라이브러리로 작업을 수행하려면 먼저 mlx_init()함수를 실행해야한다. mlx_init()함수는 mlx.h 헤더를 통해서 접근 할 수 있다.
그래픽과 소프트웨어(내가 생성한 코드)를 연결해주는 함수이며 모든 함수의 최상위 함수라고 생각해도 무방하다.

<기능>
- 소스코드와 소프트웨어를 연결

<반환값>
- 성공 : 연결 성공시 non-pointer반환
- 실패 : NULL 포인터 반환

<소스코드>
``` 
#include <mlx.h>

int     main(void)
{
    void    *mlx;

    mlx = mlx_init();
    
}
``` 