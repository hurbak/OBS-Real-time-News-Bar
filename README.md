## OBS Real-time News Bar v0.4 - 기본 설명

이 도구는 OBS Studio에서 실시간 뉴스나 공지사항을 스크롤 형태로 표시하기 위해 개발되었습니다. OBS의 "Browser" 소스에서 작동하며, 웹 기술(HTML, CSS, JavaScript)을 사용하여 뉴스 바를 렌더링합니다. [cite: 3]

작동 방식은 다음과 같습니다.

* **뉴스 소스:** 뉴스 내용은 외부 텍스트 파일(`NewsPool.txt`)에서 읽어옵니다. 이를 통해 OBS 설정을 직접 수정하지 않고도 뉴스를 업데이트할 수 있습니다. [cite: 1, 2, 3]
* **동적 표시:** 뉴스 항목은 사용자 정의가 가능한 애니메이션과 타이밍에 따라 순환하여 표시됩니다. [cite: 2, 3]
* **사용자 정의:** CSS 변수를 사용하여 글꼴, 색상, 레이아웃, 배경 등 뉴스 바의 모양을 변경할 수 있습니다. 또한 날짜와 시간을 다양한 형식으로 표시할 수 있습니다. [cite: 3]
* **하단 자막(Lower Third) 통합:** 화면 하단에 정보를 표시하는 데 사용되는 하단 자막 형태로 설계되었습니다. [cite: 3]

## OBS Real-time News Bar v0.4 - 사용 방법

1.  **뉴스 파일 준비 (`NewsPool.txt`)**

    * `NewsPool.txt`라는 이름의 텍스트 파일을 만듭니다. [cite: 1, 2, 3]
    * 파일의 각 줄은 개별 뉴스 항목이 됩니다. [cite: 1, 2, 3]
    * 줄의 시작을 해시 기호(`#`)로 하면 해당 줄은 주석으로 처리되어 무시됩니다. [cite: 1, 2, 3]
    * 예시:

    ```text
    #이것은 주석입니다.
    뉴스 샘플입니다. 첫 번째 속보입니다.
    두 번째 속보입니다.
    세 번째 속보입니다.
    ```
2.  **OBS Studio 설정**

    * OBS Studio를 엽니다.
    * 새로운 "Browser" 소스를 장면에 추가합니다.
    * Browser 소스 속성에서 다음을 수행합니다.
        * "Local file" 옵션을 선택하고 `OBS Real-time News Bar 0.4.html` 파일을 찾아서 지정합니다. [cite: 3]
        * `user-variables-setting.css` 파일의 `canvas-width` 및 `canvas-height` 변수에 따라 너비와 높이를 설정합니다 (예: 1920x1080). [cite: 3]
        * 장면을 활성화할 때 뉴스 및 설정을 다시 로드하려면 "장면이 활성화되면 브라우저 새로 고침"이 선택되어 있는지 확인합니다.
        * 필요에 따라 CSS 파일을 조정해야 할 수 있습니다. [cite: 3]
3.  **모양 사용자 정의 (`user-variables-setting.css` 및 `user-font-setting.css`)**

    * `user-variables-setting.css`: 이 파일에는 레이아웃, 색상, 타이밍 및 뉴스 바의 일반적인 모양을 제어하는 CSS 변수가 포함되어 있습니다. [cite: 3]
        * `--canvas-width` 및 `--canvas-height`: 디스플레이 영역의 전체 크기입니다. [cite: 3]
        * `--lower-third-offset-top`, `--lower-third-offset-bottom`, `--lower-third-offset-left`, 및 `--lower-third-offset-right`: 캔버스 내에서 뉴스 바의 위치와 크기를 정의합니다. [cite: 3]
        * `--show-news-header`: 뉴스 헤더를 표시하거나 숨깁니다. [cite: 3]
        * `--news-header-symbol`: 뉴스 헤더에 사용할 텍스트 또는 기호입니다 (예: "속보"). [cite: 3]
        * 색상 변수 (`--news-header-bg-color`, `--news-color` 등): 다양한 요소의 색상을 제어합니다. [cite: 3]
        * 글꼴 크기 및 글꼴 패밀리 변수 (`--news-header-font-size`, `--news-font-family` 등): 글꼴 모양을 제어합니다. [cite: 3]
        * 타이밍 변수 (`--news-animation-duration`, `--news-display-duration`, `--cycle-end-delay`): 각 뉴스 항목이 표시되는 시간과 애니메이션 속도를 제어합니다. [cite: 3]
        * `--show-clock` 및 `--show-date`: 날짜와 시간을 표시하거나 숨깁니다. [cite: 3]
        * `--datetime-position`: 날짜/시간의 위치 (왼쪽 또는 오른쪽)를 설정합니다. [cite: 3]
    * `user-font-setting.css`: 이 파일은 뉴스 바에 사용되는 글꼴을 정의합니다. `@font-face` 규칙을 추가하거나 수정하여 다른 글꼴을 사용할 수 있습니다. [cite: 3]
4.  **중요 고려 사항**

    * **파일 경로:** `NewsPool.txt` 파일이 OBS에서 액세스할 수 있는 위치에 있는지 확인합니다. 파일을 이동하면 OBS Browser 소스에서 경로를 업데이트해야 합니다. [cite: 2, 3]
    * **CSS 사용자 정의:** CSS를 어느 정도 알고 있으면 모양을 사용자 정의하는 데 도움이 됩니다. CSS 파일을 편집할 때는 잘못된 변경으로 레이아웃이 깨질 수 있으므로 주의해야 합니다. [cite: 3]
    * **성능:** Browser 소스는 OBS에서 리소스를 많이 사용할 수 있습니다. 성능 문제가 발생하면 CSS를 단순화하거나 소스의 해상도를 줄여보세요.
    * **긴 문장:** 코드에는 긴 문장이 오류를 일으킬 수 있다는 경고가 포함되어 있으므로 뉴스 항목을 비교적 간결하게 유지하는 것이 좋습니다. [cite: 2, 3]
    * **자동 업데이트:** 뉴스 바는 `NewsPool.txt` 파일의 변경 사항을 자동으로 확인하고 표시를 업데이트합니다. [cite: 3]

이 설정은 OBS Real-time News Bar를 사용하는 데 좋은 시작점이 될 것입니다. 특정 스트리밍 레이아웃과 스타일에 맞게 설정을 조정하는 것을 잊지 마세요.
