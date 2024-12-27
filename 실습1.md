# 실습 1

-------

[리소스 뷰]의 Menu에서 IDR_MAINFRAME을 선택하면 상대에 메뉴를 추가가 가능하다.

메뉴에 출력될 문자열 "그리기(&D)"를 입력후 Enter 누르면 메뉴가 만들어진다.

위와 같이 ("색상(&C)", "무늬(&P)")를 만들어 준다 그리고 부메뉴 추가를 하여 그리기에 "직선(&L)\tCtrl+L"를 입력후 추가한다.

만들어진 부메뉴 속성 창에서 [ID] ID_LINE 으로 입력하고 [프롬프트] 항목에 상태표시줄에 출력할 문자열을 "직선을 그립니다.\n직선 그리기" 를 입력한다.

위와 같이 그리기에 "원(&E)\tCtrl+E" , "베지어 곡선(&B)\tCtrl+B" 를 추가해준다.

그리고 난 후 색상에는 "선 색상(&N)" , "면 색상(&F)" 무늬에는 "오른쪽 45도(&D)" , "십자가(&C)" , "수직(&V)" 를 추가해주고 난 후

부메뉴들의 속성을 설정해준다.

| 메뉴명 | ID | 캡션 | 프롬프트 |
|---|---|---|---|
| 그리기 | ID_ELLIPSE | 원(&E)\tCtrl+E | 원을 그립니다\n원 |
| 그리기 | ID_BEZIER | 베지어 곡선(&B)\tCtrl+B | 베지어 곡선을 그립니다.\t베지어 곡선 |
| 색상 | ID_LINE_COLOR | 선 색상(&N) | 선 색상을 변경합니다.\n선 색상 | 
| 색상 | ID_FACE_COLOR | 면 색상(&F) | 면 색상을 변경합니다.\n면 색상 |
| 무늬 | ID_FDIAGONAL | 오른쪽 45도(&D) | 무늬를 변경합니다.\n오른쪽 45도 |
| 무늬 | ID_CROSS | 십자가(&C) | 무늬를 변경합니다.\n십자가 |
| 무늬 | ID_VERTICAL | 수직(&V) | 무늬를 변경합니다.\수직 |

[리소스 뷰]의 Accelerator 에서 IDR_MAINFRAME을 클릭하면 Accelerator 창이 뜨게 된다.

여기서 ID_ACCELERATOR328 을 ID_LINE 으로 변경하고 단축키를 누를 때 사용할 보조키를 Ctrl 을 True로 키를 L 로 변경한다.

위와 같은 방법으로 원과 베지어를 메뉴에서 추가하여 각 단축키에 맞게 설정을 한다.

그리고 나서 실행해보면 단축키에 관한 내용이 제대로 표시 되지 않을 수도 있다. 기본적으로 Keyboard Manager에서 초기화된 내용으로 표시되기 떄문이다.

CProject6App 클래스에서 InitInstance() 함수를 클릭하여 함수 본체로 이동 후 함수 중간 부분에 호출하고 있는 InitKeyboardManager() 함수를 주석처리 한다.

그리고 나서 [직선] 메뉴를 선택했을 때 동작할 명령 메시지 핸들러 함수를 만든다.

[클래스 마법사]에서 [클래스 이름]CProject6View 에서 [명령]에 ID_LINE에 COMMAND [메시지] 를 선택하여 추가해준다.

그리고 똑같이 나머지 메뉴들도 추가하여 다음과 같은 코드를 작성한다.

```ruby
// CProject6View 메시지 처리기


void CProject6View::OnLine()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	// 직선 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("직선을 그립니다."));
}


void CProject6View::OnEllipse()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	// dnjs 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("직선을 그립니다."));
}


void CProject6View::OnBezier()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	// 베지어 곡선 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("베지어 곡선을 그립니다."));
}


void CProject6View::OnLineColor()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	// 선 색상 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("선의 색상을 변경합니다."));
}


void CProject6View::OnFaceColor()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	// 면 색상 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("면의 색상을 변경합니다."));
}


void CProject6View::OnFdiagonal()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	// 브러쉬 스타일을 오른쪽 45도 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("오른쪽 45도 패턴으로 변경합니다."));
}


void CProject6View::OnCross()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	// 브러쉬 스타일을 십자가 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("십자가 패턴으로 변경합니다."));
}


void CProject6View::OnVertical()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
  // 브러쉬 스타일을 수직 메뉴를 선택했을 때 메시지 출력
  AfxMessageBox(_T("수직 패턴으로 변경합니다."));
}
```

![스크린샷 2024-12-26 212355](https://github.com/user-attachments/assets/9ea4b27e-1bbc-4f61-b28d-b005f005c8e8)


그리고 그리기 모드를 설정하는 멤버 변수를 추가한다.

[클래스 뷰] 에서 멤버 변수를 추가할 CProject6View 클래스를 선택한 후 [변수 추가]에서 [이름]을 m_nDrawMode로 입력후 [형식] 은 int형을 선택한다.

위와 같이 브러쉬의 무늬 패턴을 표시하는 멤버 변수를 추가한다 [이름]을 m_nHatchStyle로 입력하고 [형식] 항목은 int형을 선택한다.

그리고 그리기 모드 값을 열거형으로 선언한다 [클래스 뷰]에서 CProject6View 클래스를 더블 클릭하여 그리기 모드 값에 관한 열거형을 선언할 CProject6View 클래스의 헤더파일이 나타난다. 열거형을 다음과 같이 설정한다.

```ruby
// Project6View.h: CProject6View 클래스의 인터페이스
//

enum DRAW_MODE { LINE_MODE, ELLIPSE_MODE, BEZIER_MODE };
#pragma once
```

앞에서 만든 [그리기]와 [무늬] 메뉴에 있는 각 부메뉴의 명령 메시지 핸들러 함수로 이동하여 전에 추가한 코드인 AfxMessageBox()들을 삭제하고 메뉴가 선택됐을 때 그리기 모드 값을 변경하는 코드를 다음과 같이 추가한다.
```ruby
// CProject6View 메시지 처리기


void CProject6View::OnLine()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	//직선그리기 모드 변경
	m_nDrawMode = LINE_MODE;
}


void CProject6View::OnEllipse()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	//원 그리기 모드 변경
	m_nDrawMode = ELLIPSE_MODE;
}


void CProject6View::OnBezier()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	//베지어 곡선 그리기 모드 변경
	m_nDrawMode = BEZIER_MODE;
}


void CProject6View::OnLineColor()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	//오른쪽 45도 빗금 변경
	m_nHatchStyle = HS_FDIAGONAL;
}


void CProject6View::OnFaceColor()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	//십자가 빗금 변경
	m_nHatchStyle = HS_CROSS;
}


void CProject6View::OnFdiagonal()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	//수직 빗금 변경
	m_nHatchStyle = HS_VERTICAL;
}
```

그리고 난 후 선택된 메뉴에 체크 표시를 한다.

UPDATE_COMMAND_UI 메시지는 메뉴 항목이 표시되기 전에 보내지는 메시지로 메뉴 항목을 변경하고자 할 때 사용된다. 

[클래스 마법사] 실행 후 [클래스 이름] 항목에서 CProject6View를 선택한다. [명령] 항목에서 ID_LINE을 선택한 후 [메시지] 항목에서 UPDATE_COMMAND_UI를 선택하여 메시지 핸들러 함수를 추가한다.

그리고 나머지 [그리기] 메뉴에 대해 사용자 인터페이스 갱신 메시지 핸들러 함수도 만들고 다음과 같이 코드를 작성한다.

```ruby
void CProject6View::OnUpdateLine(CCmdUI* pCmdUI)
{
	// TODO: 여기에 명령 업데이트 UI 처리기 코드를 추가합니다.
	//직선 그리기 모드이면 메뉴에 체크 표시
	pCmdUI->SetCheck(m_nDrawMode == LINE_MODE ? 1 : 0);
}


void CProject6View::OnUpdateEllipse(CCmdUI* pCmdUI)
{
	// TODO: 여기에 명령 업데이트 UI 처리기 코드를 추가합니다.
	pCmdUI->SetCheck(m_nDrawMode == ELLIPSE_MODE ? 1 : 0);
}


void CProject6View::OnUpdateBezier(CCmdUI* pCmdUI)
{
	// TODO: 여기에 명령 업데이트 UI 처리기 코드를 추가합니다.
	pCmdUI->SetCheck(m_nDrawMode == BEZIER_MODE ? 1 : 0);
}
```

그리고 나서 실행시키면 다음과 같이 메뉴 항목을 선택했을 때 체크표시가 된다.

![image](https://github.com/user-attachments/assets/a3323d2d-84f9-46d9-b985-df07e6a78363)


