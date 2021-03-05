# Project Title / 42seoul_cube3d_miniLibx 사용법

# contents  

1. 소개
2. 시작함수
3. 윈도우(디스플레이) 관리 함수

# 소개

42seoul subject 중 cube_3d라는 과제가 있으며 이 과제를 수행하기 위해서는 miniLibx 사용법을 알아야하며 
miniLibx가 제공하는 함수들의 사용법을 알아야지 cube_3d를 하나하나 만듬에 있어서 로직 구조를 어떻게 해야할지 설계를 할 수 있다.
그럼으로 제공하는 함수에 대해 자세히 정리해보고자 따로 사용법에 대해서 설명하려한다.


# 시작함수

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
만약 이 코드를 실행하면 아무일도 일어나지 않습니다. 왜냐면 이 함수는 소스코드와 디스플레이를 연결만 할뿐, 디스틀레이를 출력하는 함수는 따로 있기 때문입니다.
만약, 디스플레이를 출력하고자 한면 mlx_new_window()함수를 사용해야합니다.

# 윈도우(디스플레이) 관리 함수

## mlx_new_window
화면을 띄우는데 도움을 주는 함수입니다.

<원형>
```
void *mlx_new_window(void *mlx_ptr, int size_x, int size_y, char *title)
```
< 매개변수 >
mlx_ptr : 연결 식별자(위에서 mlx_init() 함수와 연결되는 것을 보았다.)
size_x, size_y : 화면의 가로 세로 크기를 결정한다.
title : 창의 타이틀 바에 씌여징 문자열이다.

< 반환값 >
함수의 init함수와 연결 확인 여부 를 반환 연결 실패시 non-null포인터 반환
생성 실패시 NULL반환 

## mlx_clear_window
<원형>
```
int     mlx_destroy_window(void *mlx_ptr, void *wind_ptr)
```
miniLibx를 처음 가동하면 검은색 화면이 나타난다. 즉, 검은화면에 우리가 그림을 그려 넣기 때문에 clear함수는 검은화면으로 시작하게 끔 도와준다.

< 매개변수 >
상황에 따라 디스플레이 매개변수를 넣을 것

< 반환값 >
따로 없음


## mlx_destroy_window
<원형>
```
int	mlx_destroy_window(void	*mlx_ptr, void *wind_ptr)
```
<매개변수>
mlx_clear_window와 같다.

<반환값>
따로 없음

mlx_clear_window와 mlx_destroy_window함수 둘다 화면을 검은색으로 지우고 지정된 창을 삭제하는 역할을 합니다.


# 픽셀로 이미를 그려주는데 도와주는 함수들

miniLibx를 통해서 디스플레이에 어떻게 픽셀을 통해 원하는 화면을 표현할 수 있는지 알아보는 과정입니다. 여기서 설명하려는 함수들은 원하는 그림을 표현하는데 있어서 최적화된 함수들을 설명하겠습니다.


## mlx_new_image
```
void    *mlx_new_image(void *mlx_ptr, int width, int height)
```
사용자가 원하는 이미지를 메모리에 생성시킵니다.(다시말해, 사용자가 원하는 이미지를 바로 화면에 디스플레이 할 수 없습니다. 일단 먼저 소스코드상의 메모리에 장착 시킨 후 디스플레이의 크기에 맞게 연출하게 됩니다. 그러기 위해서는 먼저 이미지를 꺼내와서 메모리공간에 초기화를 해줘야합니다.)

<매개변수>
- 이미지를 가리키는 포인터
- 이미지 사이즈를 위한 가로, 세로 

<반환값>
- 실패시 NULL리턴


## mlx_put_image_to_window
```
mlx_put_image_to_window(void *mlx_ptr, void *win_ptr, void *img_ptr, int x, int y)
```
사용자가 원하는 이미지를 메모리에 초기화 시키는게 mlx_new_image의 역할 이라면
mlx_put_image_to_window는 디스플레이에 연결하여 원하는 위치에 화면을 출력해줍니다.

<매개변수>
- mlx_ptr : 출력하려는 이미지 포인터
- win_ptr : 출력하려는 이미지 창(mlx_new_window로 만든 창을 가리키는 포인터)을 가리키는 포인터
- img_ptr : 사용하려는 이미지를 지정합니다.(mlx_new_image를 이용해 초기화한 메모리를 가리킴)
- x, y = 창 내부에 이미지를 출력 시킬 위치를 가리킨다.

<반환값>
- 로드 실패할 시 NULL을 출력