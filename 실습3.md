# 실습 3

-------

상태 표시줄(Status Bar)<br>
상태 표시줄은 메인 프레임 하단 부에 위치하여 특정 항목을 선택하면 해당 항목의 도움말이 출력되는 형태의 윈도우를 말한다. 이들 윈도우는 그래픽으로 표시될 수도 있지만, 일반적으로 문자열 형태로 정보를 나타낸다.

[리소스 뷰]의 Project6.rc을 오른쪽 마우스 버튼을 눌러 [리소스 기호]를 마우스로 눌러 [리소스 기호] 대화상자를 실행시킨다.

[리소스 기호] 대화사자에서 팬에 설정할 ID를 만들기 위해 [새로 만들기] 를 하여 ID를ID_INDICATOR_POINT로 설정한다.

새로 만든 팬에 출력할 초기 문자열과 크기를 정의하기 위해 [리소스 뷰]의 String Table에서 새로운걸 만들어 [속성]창의 ID를 ID_INDICATOR_POINT로 하고 [캡션] 항목에 초기 문자열("마우스:    X좌표    Y좌표")을 입력한다.

상태 표시줄에 팬을 추가 하기 위해 [클래스 뷰]에서 팬의 ID를 추가할 CMainFrame 클래스의 멤버 변수를 하나 선택하여 더블 클릭하여 소스 파일의 윗부분으로 이동한다.<br>
CMainFrame 클래스의 상태 표시줄을 분할하는 지시자 설정 부분에 팬의 ID를 추가한다.

```ruby
static UINT indicators[] =
{
	ID_SEPARATOR,           // 상태 줄 표시기
	ID_INDICATOR_POINT,     // 새로운 팬의 ID 추가
	ID_INDICATOR_CAPS,
	ID_INDICATOR_NUM,
	ID_INDICATOR_SCRL,
};
```

그리고 나서 CMainFrame 클래스의 OnCreate 함수에서 지시자에 설정한 분할될 영역의 수만큼 상태 표시줄을 크기에 맞게 나누어주기 위해 SetIndicators()함수를 호출한다.

```ruby
int CMainFrame::OnCreate(LPCREATESTRUCT lpCreateStruct)
{
  ......
	m_wndStatusBar.SetIndicators(indicators, sizeof(indicators)/sizeof(UINT));
	// 마우스의 좌표를 출력할 상태 바의 위치, ID, 크기를 설정한다.
	m_wndStatusBar.SetPaneInfo(1, ID_INDICATOR_POINT, SBPS_NORMAL, 200);
  ......
}
```

그리고 실행하면 다음과 같이 오른쪽 하단에 새로 생성한 팬과 설정한 초기 문자열이 보인다.

![image](https://github.com/user-attachments/assets/d33584a3-938b-4f5a-8d51-c1259f830649)

상태 표시줄에 마우스 좌표를 출력하기 위해 [클래스 마법사]를 실행하여 [클래스 이름] 항목에서 CProject6View을 선택하고 [메시지]항목에서 WM_MOUSEMOVE을 선택하여 메시지 핸들러 함수를 만든다. 그리고 나서 다음과 같은 코드를 작성한다.

```ruby
void CProject6View::OnMouseMove(UINT nFlags, CPoint point)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.
	// 메인프레임의 포인터 얻음
	CMainFrame* pFrame = (CMainFrame*)AfxGetMainWnd();

	CString strPoint;
	strPoint.Format(_T("마우스 위치 x : %d, y : %d"), point.x, point.y);

	//새로 추가한 팬에 마우스 위치 출력
	pFrame->m_wndStatusBar.SetPaneText(1, strPoint);

	CView::OnMouseMove(nFlags, point);
}
```

w_wndStatusBar는 CMainFrame 클래스의 멤버 변수이므로 AfxGetMainWnd() 함수를 이용하여 얻어진 CMainFrame 클래스의 인스턴스 포인터(ex PFrame)를 이용하여 접근해야 한다. 이때,CMainFrame 클래스의 외부인 CProject6View 클래스에서<br>
CMainFrame 클래스의 멤버를 참조하려면 m_wndStatusBar가 CMainFrame 클래스의 public 멤버로 선언되어 있어야 한다. 또한 CProject6View 클래스의 소스파일에 CMainFrame 클래스의 헤더파일을 include 시켜야한다.

CMainFrame의 헤더파일에서 CMFCStatusBar 클래스의 객체를 protected 에서 public으로 수정한다.

그리고 CProjectView 클래스에서 CMainFrame 클래스의 헤더파일을 include 시킨다.

```ruby
#include "MainFrm.h"
```

[최종]
![image](https://github.com/user-attachments/assets/eeff6962-31f7-4ebc-99ba-d119f0180269)
