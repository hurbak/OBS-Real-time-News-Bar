# OBS Real-time News Bar (v0.41)

This tool was developed to display real-time news or announcements in a scrolling format within OBS Studio. It works as a "Browser" source in OBS, rendering the news bar using web technologies (HTML, CSS, JavaScript).

## How it Works

* **News Source:** News content is read from an external text file (`NewsPool.txt`). This allows you to update the news without directly modifying the OBS settings. The file should be located at `/newsPool/NewsPool.txt`.
* **Dynamic Display:** News items are displayed cyclically according to customizable animations and timings.
* **Customization:** You can change the appearance of the news bar, such as fonts, colors, layout, background, animation types, and timings, using CSS variables. You can also display the date and time in various formats.
* **Lower Third Integration:** It is designed as a lower third, used to display information at the bottom of the screen.

## What's New in v0.41

Version 0.41 brings several significant improvements and structural changes:

* **Fixed Gradient Overlay Bug:** Resolved an issue where the full-screen gradient background was not applied correctly.
* **Improved Clock Stability with Fixed-Width Font:** Introduced specific fixed-width fonts for the clock numbers (`font-variant-numeric: tabular-nums;`) to prevent the clock's width from fluctuating when digits change, ensuring a more stable layout. Vertical alignment of clock numbers and colons can now be fine-tuned more precisely using dedicated offset variables.
* **Added News Animation Options:** Implemented new animation types for news transitions, allowing for more diverse visual effects. (Configurable via `--news-animation-type`).
* **Relocated `newsPool.txt`:** The required location for the news file has been moved to a dedicated folder: `./newsPool/NewsPool.txt`. When updating from a previous version, you need to update the file path.
* **Code Structure Refinement:** Styles and scripts have been separated into external CSS (`style-041.css`, `user-variables-setting-041.css`, `user-font-setting-041.css`) and JavaScript (`script-041.js`) files. This enhances code organization and makes customization easier.
* **Enhanced Clock Format Options:** Added support for both HH:MM and HH:MM:SS clock formats, selectable via a new variable (`--time-format-option`). The HH:MM format includes a blinking colon option.
* **Detailed Vertical Alignment for Clock:** Added `--breaking-news-clock-num-offset-top` and `--breaking-news-clock-colon-offset-top` variables for precise vertical positioning adjustments of clock digits and colons, addressing potential alignment issues caused by different fonts.

## How to Use

1.  **Prepare News File (`NewsPool.txt`)**
    * Create a text file named `NewsPool.txt`.
    * Each line in the file will be a separate news item.
    * If a line starts with a hash symbol (`#`), it will be treated as a comment and ignored.
    * Example:

        ```text
        # This is a comment.
        This is a news sample. The first breaking news.
        This is the second breaking news.
        This is the third breaking news.
        ```
2.  **OBS Studio Setup**
    * Open OBS Studio.
    * Add a new "Browser" source to your scene.
    * In the Browser Source properties, do the following:
        * Select the "Local file" option and browse to the **`OBS Real-time News Bar 0.41.html`** file in the folder you extracted the files to.
        * **Width and Height:** It is recommended to set the width and height to match the `--canvas-width` and `--canvas-height` variables in the `user-variables-setting-041.css` file (e.g., 1920x1080).
        * **"Refresh browser when scene becomes active":** Ensure this option is checked to reload news and settings when the scene is activated.
3.  **Customize Appearance (`user-variables-setting-041.css` and `user-font-setting-041.css`)**
    * `user-variables-setting-041.css`: This file contains CSS variables that control the layout, colors, timings, and general appearance of the news bar. Refer to the **User Customization Variables Explained** section below to modify the values as desired.
    * `user-font-setting-041.css`: This file defines the fonts used in the news bar. You can add or modify `@font-face` rules to use different fonts or apply web fonts.

## User Customization Variables Explained (`user-variables-setting-041.css`)

This file provides a variety of CSS variables that allow you to precisely control the appearance and behavior of the news bar. Detailed explanations for each variable are as follows:

### 1. General Layout Settings (Canvas & Lower Third Bar)

* `--canvas-width`: The total width of the OBS Browser source (in px).
* `--canvas-height`: The total height of the OBS Browser source (in px).
* `--gradient-color-stop-1-value`: The RGBa value for the first color stop of the overall canvas background gradient (e.g., `255, 0, 0, 0.5` - red with 50% transparency).
* `--gradient-color-stop-2-value`: The RGBa value for the second color stop of the overall canvas background gradient.
* `--gradient-color-stop-3-value`: The RGBa value for the third color stop of the overall canvas background gradient.
* `--gradient-color-stop-1-position`: The position (%) of the first color stop.
* `--gradient-color-stop-2-position`: The position (%) of the second color stop.
* `--gradient-color-stop-3-position`: The position (%) of the third color stop.
* `--canvas-gradient`: The `linear-gradient` CSS value for the overall canvas background generated using the color and position variables defined above. Generally, you modify the color and position variables rather than this variable itself.
* `--lower-third-offset-top`: The offset (in px) from the top of the canvas to the lower third bar.
* `--lower-third-offset-bottom`: The offset (in px) from the bottom of the canvas to the lower third bar.
* `--lower-third-offset-left`: The offset (in px) from the left of the canvas to the lower third bar.
* `--lower-third-offset-right`: The offset (in px) from the right of the canvas to the lower third bar.
* `--lower-third-width`: The calculated width of the lower third bar (`calc(var(--canvas-width) - var(--lower-third-offset-left) - var(--lower-third-offset-right))`). Do not modify this variable directly.
* `--lower-third-height`: The calculated height of the lower third bar (`calc(var(--canvas-height) - var(--lower-third-offset-top) - var(--lower-third-offset-bottom))`). Do not modify this variable directly.
* `--lower-third-spacing`: The gap (in px) between internal elements of the lower third bar (date/time, header, news text container).

### 2. News Settings

* `--show-news-header`: Sets whether to display the news header (e.g., "BREAKING"). Use `Y` or `N`.
* `--news-header-symbol`: The text or symbol to be displayed in the news header (e.g., `"속보"`, `"BREAKING"`). Include quotation marks around the value.
* `--news-header-bg-color`: The background color of the news header (RGBa value).
* `--news-header-padding-top`, `--news-header-padding-right`, `--news-header-padding-bottom`, `--news-header-padding-left`: Top, right, bottom, and left padding (in px) inside the news header.
* `--news-header-border-radius`: The border radius (in px) for the corners of the news header.
* `--news-container-bg-color`: The background color of the container where the news text is displayed (RGBa value).
* `--news-container-padding-top`, `--news-container-padding-right`, `--news-container-padding-bottom`, `--news-container-padding-left`: Top, right, bottom, and left padding (in px) inside the news text container.
* `--news-container-border-radius`: The border radius (in px) for the corners of the news text container.

### 3. Datetime (Clock/Date) Settings

* `--show-clock`: Sets whether to display the clock (`Y` or `N`).
* `--show-date`: Sets whether to display the date (`Y` or `N`).
* `--time-format-option`: Selects the clock display format.
    * `1`: HH:MM format (includes blinking colon)
    * `2`: HH:MM:SS format (colon is always displayed)
* `--datetime-position`: Sets the position of the date/time section (`L` - Left, `R` - Right). If set to Left, it will be displayed before the news header and news text container.
* `--datetime-bg-color`: The background color of the date/time section (RGBa value).
* `--datetime-padding-top`, `--datetime-padding-right`, `--datetime-padding-bottom`, `--datetime-padding-left`: Top, right, bottom, and left padding (in px) inside the date/time section.
* `--datetime-border-radius`: The border radius (in px) for the corners of the date/time section.
* `--breaking-news-clock-num-offset-top`: Offset (in px) for fine-tuning the vertical alignment of clock numbers (`0-9`). Positive values move the numbers downwards.
* `--breaking-news-clock-colon-offset-top`: Offset (in px) for fine-tuning the vertical alignment of clock colons (`:`). Positive values move the colons downwards.

### 4. Animation & Timing Settings

* `--news-animation-type`: Selects how news items appear.
    * `1`: Fade-in and Slide-up (original animation)
    * `2`: Text Horizontal Reveal effect
    * `3`: (If implemented) Continuous scroll of all news items combined.
* `--news-animation-duration`: The duration (in milliseconds, ms) of the news item appearance animation and CSS transition.
* `--news-display-duration`: The time (in milliseconds, ms) each news item is displayed on the screen. (May not be used directly for Type 3 continuous scroll).
* `--cycle-end-delay`: The delay (in milliseconds, ms) after cycling through all news items before the next cycle restarts. (May be used for file change check interval in Type 3 continuous scroll).
* `--news-hide-duration`: The duration (in milliseconds, ms) of the news item hide animation.
* `--news-scroll-speed`: (If Type 3 continuous scroll is implemented) The speed of the continuous scroll animation (in pixels per second). Higher values result in faster scrolling.
* `--news-check-interval`: (If Type 3 continuous scroll is implemented) The interval (in milliseconds, ms) for checking for news file changes while scrolling.

### 5. Font Settings Variables

* `--global-font-family`: The default font family to be applied to the entire news bar. Use font family names defined in `user-font-setting-041.css`'s `@font-face` rules or system font names. You can specify a fallback list of fonts separated by commas.
* `--breaking-news-clock-font-family`: The font family to be applied specifically to clock numbers and colons. It is recommended to use a font that supports `tabular-nums` for fixed-width digits. Use a dedicated clock font family name defined in `user-font-setting-041.css`.
* `--news-header-font-size`: The font size (in px) for the news header.
* `--news-header-font-family`: The font family to use for the news header. Can use `var(--global-font-family)` or specify a different font name.
* `--news-header-font-weight`: The font weight for the news header text (e.g., `300`, `normal`, `bold`, `700`, etc.). The font you use must support the specified weight.
* `--news-header-color`: The text color for the news header (RGBa value).
* `--datetime-font-size`: The font size (in px) for the date and time section (excluding the clock digits/colons).
* `--datetime-font-family`: The font family to use for the date and time section (excluding the clock digits/colons).
* `--datetime-font-weight`: The font weight for the date and time section (excluding the clock digits/colons).
* `--datetime-color`: The text color for the date and time section (excluding the clock digits/colons) (RGBa value).
* `--breaking-news-clock-font-size`: The font size (in px) to be applied specifically to clock numbers and colons. Can be set differently from `--datetime-font-size`.
* `--breaking-news-clock-color`: The text color for clock numbers and colons (RGBa value). Can be set differently from `--datetime-color`.

## Important Considerations

* **File Path:** Ensure that the `newsPool/NewsPool.txt` file is located relative to the HTML file (`OBS Real-time News Bar 0.41.html`) loaded in the OBS Browser source, specifically in the `./newsPool/` directory. If you move the files or change the OBS source path, you must update the path accordingly.
* **CSS Customization:** Modifying CSS variables is relatively safe, but be cautious when directly editing main CSS files like `style-041.css` as incorrect changes can break the layout.
* **Performance:** Browser sources can use resources in OBS. If you encounter performance issues, try simplifying the CSS or reducing the source's resolution.
* **Long Sentences:** Depending on the animation method, very long news items might cause layout issues. This is especially true for Type 3 continuous scroll where the total text length can be significant.
* **Automatic Updates:** The news bar automatically checks for changes in the `newsPool/NewsPool.txt` file periodically and updates the display. (For Type 3 scroll, the check interval is controlled by the `--news-check-interval` variable).

This updated README should help users of the OBS Real-time News Bar v0.41 understand the new features and settings and effectively customize the appearance.

---

# OBS Real-time News Bar (v0.41)

이 도구는 OBS Studio에서 실시간 뉴스나 공지사항을 유연하게 스크롤 형태로 표시하기 위해 개발되었습니다. OBS의 "Browser" 소스에서 작동하며, 웹 기술(HTML, CSS, JavaScript)을 사용하여 뉴스 바를 렌더링합니다.

## 작동 방식

* **뉴스 소스:** 뉴스 내용은 외부 텍스트 파일(`NewsPool.txt`)에서 읽어옵니다. 이를 통해 OBS 설정을 직접 수정하지 않고도 뉴스를 업데이트할 수 있습니다. 파일은 `/newsPool/NewsPool.txt` 경로에 위치해야 합니다.
* **동적 표시:** 뉴스 항목은 사용자 정의가 가능한 다양한 애니메이션과 타이밍에 따라 순환하여 표시됩니다.
* **사용자 정의:** CSS 변수를 사용하여 레이아웃, 색상, 글꼴, 배경, 애니메이션 타입 및 타이밍 등 뉴스 바의 거의 모든 시각적 요소를 변경할 수 있습니다.
* **날짜 및 시간:** 날짜와 시간을 원하는 형식으로 표시할 수 있으며, 위치 및 글꼴을 별도로 설정할 수 있습니다.
* **하단 자막(Lower Third) 통합:** 화면 하단에 정보를 표시하는 데 사용되는 하단 자막 형태로 설계되었습니다.

## 0.41 버전의 새로운 기능

버전 0.41에서는 안정성, 유연성 및 코드 구조에 대한 몇 가지 중요한 개선이 이루어졌습니다.

* **그라디언트 오버레이 버그 수정:** 전체 화면 그라디언트 배경이 올바르게 적용되지 않던 문제를 수정했습니다.
* **고정폭 폰트로 시계 안정성 향상:** 가변폭 폰트 사용 시 숫자가 변경될 때 시계 섹션의 너비가 변동되는 문제를 방지하기 위해 시계 숫자 및 콜론에 대해 특정 고정폭 폰트(`font-variant-numeric: tabular-nums;`)를 도입했습니다. 이를 통해 시계 표시의 레이아웃 안정성이 확보되었습니다. 또한, 시계 숫자 및 콜론의 세로 정렬을 전용 오프셋 변수를 사용하여 더욱 정밀하게 조정할 수 있게 되었습니다.
* **뉴스 애니메이션 옵션 추가:** 새로운 뉴스 전환 애니메이션 타입이 구현되어 더욱 다양한 시각 효과를 사용할 수 있습니다. (`--news-animation-type` 변수로 설정 가능).
* **`newsPool.txt` 파일 위치 변경:** 뉴스 데이터 파일의 필수 위치가 전용 폴더인 `./newsPool/NewsPool.txt`로 변경되었습니다. 이전 버전에서 업데이트하는 경우 파일 경로를 업데이트해야 합니다.
* **코드 구조 개선:** 스타일과 스크립트가 외부 CSS (`style-041.css`, `user-variables-setting-041.css`, `user-font-setting-041.css`) 및 JavaScript (`script-041.js`) 파일로 분리되었습니다. 이를 통해 코드 구성이 개선되고 사용자 정의가 용이해졌습니다.
* **시계 형식 옵션 확장:** HH:MM 및 HH:MM:SS 시계 형식을 모두 지원하며, 새로운 변수(`--time-format-option`)로 선택할 수 있습니다. HH:MM 형식에는 콜론 깜빡임 옵션이 포함됩니다.
* **시계의 상세 세로 정렬:** 글꼴 차이로 인해 발생할 수 있는 잠재적인 정렬 문제를 해결하기 위해 시계 숫자 및 콜론의 정밀한 세로 위치 조정을 위한 `--breaking-news-clock-num-offset-top` 및 `--breaking-news-clock-colon-offset-top` 변수가 추가되었습니다.

## 사용 방법

1.  **파일 준비**
    * 압축 파일을 다운로드하고 모든 내용을 원하는 폴더에 압축 해제합니다.
    * `newsPool` 폴더 안에 `NewsPool.txt` 파일을 만듭니다.
    * **`NewsPool.txt`** 파일에 표시하려는 뉴스 항목을 각 줄에 작성합니다.
        * 줄의 시작을 해시 기호(`#`)로 하면 해당 줄은 주석으로 처리되어 무시됩니다.
        * 예시:

            ```text
            #이것은 주석입니다.
            뉴스 샘플입니다. 첫 번째 속보입니다.
            두 번째 속보입니다.
            세 번째 속보입니다.
            ```
2.  **OBS Studio 설정**
    * OBS Studio를 엽니다.
    * 장면에 새로운 "Browser" 소스를 추가합니다.
    * Browser 소스 속성에서 다음을 설정합니다.
        * "Local file" 옵션을 선택하고 압축 해제한 폴더 안에 있는 **`OBS Real-time News Bar 0.41.html`** 파일을 찾아서 지정합니다.
        * **너비 (Width) 및 높이 (Height):** `user-variables-setting-041.css` 파일에 설정된 `--canvas-width` 및 `--canvas-height` 변수 값과 동일하게 설정하는 것이 좋습니다 (예: 1920x1080).
        * **"장면이 활성화되면 브라우저 새로 고침":** 이 옵션을 선택하여 장면 전환 시 뉴스 및 설정을 다시 로드하도록 합니다.
3.  **모양 사용자 정의 (`user-variables-setting-041.css` 및 `user-font-setting-041.css`)**
    * `user-variables-setting-041.css`: 이 파일에는 뉴스 바의 레이아웃, 색상, 타이밍, 애니메이션 등 대부분의 설정을 제어하는 CSS 변수들이 포함되어 있습니다. 아래의 **사용자 정의 변수 설명** 섹션을 참고하여 원하는 대로 값을 수정하세요.
    * `user-font-setting-041.css`: 이 파일은 뉴스 바에 사용되는 글꼴을 정의합니다. `@font-face` 규칙을 추가하거나 수정하여 다른 글꼴을 사용하거나 웹 폰트를 적용할 수 있습니다.

## 사용자 정의 변수 설명 (`user-variables-setting-041.css`)

이 파일은 뉴스 바의 모양과 동작을 세부적으로 제어할 수 있는 다양한 CSS 변수를 제공합니다. 각 변수에 대한 자세한 설명은 다음과 같습니다.

### 1. 일반 레이아웃 설정 (캔버스 및 하단 자막 바)

* `--canvas-width`: OBS 브라우저 소스의 전체 너비 (px)입니다.
* `--canvas-height`: OBS 브라우저 소스의 전체 높이 (px)입니다.
* `--gradient-color-stop-1-value`: 전체 캔버스 배경 그라디언트의 첫 번째 색상 정지점의 RGBa 값 (예: `255, 0, 0, 0.5` - 빨간색 50% 투명).
* `--gradient-color-stop-2-value`: 전체 캔버스 배경 그라디언트의 두 번째 색상 정지점의 RGBa 값.
* `--gradient-color-stop-3-value`: 전체 캔버스 배경 그라디언트의 세 번째 색상 정지점의 RGBa 값.
* `--gradient-color-stop-1-position`: 첫 번째 색상 정지점의 위치 (%)입니다.
* `--gradient-color-stop-2-position`: 두 번째 색상 정지점의 위치 (%)입니다.
* `--gradient-color-stop-3-position`: 세 번째 색상 정지점의 위치 (%)입니다.
* `--canvas-gradient`: 위에서 정의한 색상 및 위치 변수를 사용하여 생성되는 전체 캔버스 배경의 `linear-gradient` CSS 값입니다. 일반적으로 이 변수 자체를 직접 수정하기보다는 위의 색상 및 위치 변수를 수정합니다.
* `--lower-third-offset-top`: 캔버스 상단에서 하단 자막 바까지의 오프셋 (px)입니다.
* `--lower-third-offset-bottom`: 캔버스 하단에서 하단 자막 바까지의 오프셋 (px)입니다.
* `--lower-third-offset-left`: 캔버스 왼쪽에서 하단 자막 바까지의 오프셋 (px)입니다.
* `--lower-third-offset-right`: 캔버스 오른쪽에서 하단 자막 바까지의 오프셋 (px)입니다.
* `--lower-third-width`: 계산된 하단 자막 바의 너비입니다 (`calc(var(--canvas-width) - var(--lower-third-offset-left) - var(--lower-third-offset-right))`). 이 변수는 직접 수정하지 않습니다.
* `--lower-third-height`: 계산된 하단 자막 바의 높이입니다 (`calc(var(--canvas-height) - var(--lower-third-offset-top) - var(--lower-third-offset-bottom))`). 이 변수는 직접 수정하지 않습니다.
* `--lower-third-spacing`: 하단 자막 바 내부 요소들 (날짜/시간, 헤더, 뉴스 텍스트 컨테이너) 사이의 간격 (px)입니다.

### 2. 뉴스 설정

* `--show-news-header`: 뉴스 헤더 (예: "속보")를 표시할지 여부를 설정합니다 (`Y` 또는 `N`).
* `--news-header-symbol`: 뉴스 헤더에 표시될 텍스트 또는 기호입니다 (예: `"속보"`, `"BREAKING"`). 따옴표를 포함하여 값을 설정합니다.
* `--news-header-bg-color`: 뉴스 헤더의 배경 색상입니다 (RGBa 값).
* `--news-header-padding-top`, `--news-header-padding-right`, `--news-header-padding-bottom`, `--news-header-padding-left`: 뉴스 헤더 내부의 상하좌우 패딩 (px)입니다.
* `--news-header-border-radius`: 뉴스 헤더의 모서리 둥글기 (px)입니다.
* `--news-container-bg-color`: 뉴스 텍스트가 표시되는 컨테이너의 배경 색상입니다 (RGBa 값).
* `--news-container-padding-top`, `--news-container-padding-right`, `--news-container-padding-bottom`, `--news-container-padding-left`: 뉴스 텍스트 컨테이너 내부의 상하좌우 패딩 (px)입니다.
* `--news-container-border-radius`: 뉴스 텍스트 컨테이너의 모서리 둥글기 (px)입니다.

### 3. 날짜 및 시간 설정

* `--show-clock`: 시계를 표시할지 여부를 설정합니다 (`Y` 또는 `N`).
* `--show-date`: 날짜를 표시할지 여부를 설정합니다 (`Y` 또는 `N`).
* `--time-format-option`: 시계 표시 형식을 선택합니다.
    * `1`: HH:MM 형식 (콜론 깜빡임 포함)
    * `2`: HH:MM:SS 형식 (콜론 항상 표시)
* `--datetime-position`: 날짜/시간 섹션의 위치를 설정합니다 (`L` - 왼쪽, `R` - 오른쪽). 왼쪽으로 설정하면 뉴스 헤더 및 뉴스 텍스트 컨테이너보다 먼저 표시됩니다.
* `--datetime-bg-color`: 날짜/시간 섹션의 배경 색상입니다 (RGBa 값).
* `--datetime-padding-top`, `--datetime-padding-right`, `--datetime-padding-bottom`, `--datetime-padding-left`: 날짜/시간 섹션 내부의 상하좌우 패딩 (px)입니다.
* `--datetime-border-radius`: 날짜/시간 섹션의 모서리 둥글기 (px)입니다.
* `--breaking-news-clock-num-offset-top`: 시계 숫자(`0-9`)의 세로 정렬 미세 조정을 위한 오프셋 (px)입니다. 양수 값은 아래로 이동합니다.
* `--breaking-news-clock-colon-offset-top`: 시계 콜론(`:`)의 세로 정렬 미세 조정을 위한 오프셋 (px)입니다. 양수 값은 아래로 이동합니다.

### 4. 애니메이션 및 타이밍 설정

* `--news-animation-type`: 뉴스 항목이 나타나는 방식을 선택합니다.
    * `1`: 페이드인 및 슬라이드업
    * `2`: 텍스트 가로 Reveal 효과
    * `3`: (만약 구현했다면) 모든 뉴스 항목을 합쳐서 연속 스크롤
* `--news-animation-duration`: 뉴스 항목이 나타나는 애니메이션 및 CSS 트랜지션의 지속 시간 (밀리초, ms)입니다.
* `--news-display-duration`: 각 뉴스 항목이 화면에 표시되는 시간 (밀리초, ms)입니다. (Type 3 연속 스크롤 시에는 직접 사용되지 않을 수 있습니다.)
* `--cycle-end-delay`: 모든 뉴스 항목을 한 번 순환한 후 다음 사이클을 시작하기 전의 대기 시간 (밀리초, ms)입니다. (Type 3 연속 스크롤 시에는 파일 변경 확인 간격 등으로 사용될 수 있습니다.)
* `--news-hide-duration`: 뉴스 항목이 사라지는 애니메이션의 지속 시간 (밀리초, ms)입니다.
* `--news-scroll-speed`: (만약 Type 3 연속 스크롤을 구현했다면) 연속 스크롤 애니메이션의 속도 (픽셀/초)입니다. 값이 클수록 스크롤이 빨라집니다.
* `--news-check-interval`: (만약 Type 3 연속 스크롤을 구현했다면) 연속 스크롤 중에 뉴스 파일 변경을 확인하는 간격 (밀리초, ms)입니다.

### 5. 글꼴 설정 변수

* `--global-font-family`: 전체 뉴스 바에 기본적으로 적용될 글꼴 패밀리입니다. `user-font-setting-041.css`에 정의된 `@font-face` 이름 또는 시스템 글꼴 이름을 사용합니다. 여러 글꼴을 쉼표로 구분하여 대체 글꼴 목록을 지정할 수 있습니다.
* `--breaking-news-clock-font-family`: 시계 숫자 및 콜론에만 적용될 글꼴 패밀리입니다. 시계 숫자의 가로폭이 고정되는 `tabular-nums`를 지원하는 글꼴을 사용하는 것이 좋습니다. `user-font-setting-041.css`에 정의된 시계 전용 `@font-face` 이름을 사용합니다.
* `--news-header-font-size`: 뉴스 헤더의 글꼴 크기 (px)입니다.
* `--news-header-font-family`: 뉴스 헤더에 사용할 글꼴 패밀리입니다. `--global-font-family`를 사용하거나 특정 글꼴 이름을 지정할 수 있습니다.
* `--news-header-font-weight`: 뉴스 헤더 글꼴의 두께입니다 (예: `300`, `normal`, `bold`, `700` 등). 사용하려는 폰트가 해당 두께를 지원해야 합니다.
* `--news-header-color`: 뉴스 헤더 텍스트 색상입니다 (RGBa 값).
* `--datetime-font-size`: 날짜 및 시간 섹션 (시계 제외)의 글꼴 크기 (px)입니다.
* `--datetime-font-family`: 날짜 및 시간 섹션 (시계 제외)에 사용할 글꼴 패밀리입니다.
* `--datetime-font-weight`: 날짜 및 시간 섹션 (시계 제외) 글꼴의 두께입니다.
* `--datetime-color`: 날짜 및 시간 섹션 (시계 제외) 텍스트 색상입니다 (RGBa 값).
* `--breaking-news-clock-font-size`: 시계 숫자 및 콜론에만 적용될 글꼴 크기 (px)입니다. `--datetime-font-size`와 다르게 설정할 수 있습니다.
* `--breaking-news-clock-color`: 시계 숫자 및 콜론에만 적용될 텍스트 색상입니다 (RGBa 값). `--datetime-color`와 다르게 설정할 수 있습니다.

## 중요 고려 사항

* **파일 경로:** `newsPool/NewsPool.txt` 파일이 OBS Browser 소스가 로드된 HTML 파일 (`OBS Real-time News Bar 0.41.html`)을 기준으로 `./newsPool/` 경로에 있는지 확인해야 합니다. 파일을 이동하거나 OBS 소스 경로를 변경한 경우 해당 경로를 수정해야 합니다.
* **CSS 사용자 정의:** CSS 변수 수정은 비교적 안전하지만, `style-041.css`와 같은 메인 CSS 파일을 직접 수정할 때는 잘못된 변경으로 레이아웃이 깨질 수 있으므로 주의해야 합니다.
* **성능:** Browser 소스는 OBS에서 리소스를 사용할 수 있습니다. 성능 문제가 발생하면 CSS를 단순화하거나 소스의 해상도를 줄여보세요.
* **뉴스 항목 길이:** 코드의 애니메이션 방식에 따라 너무 긴 뉴스 항목은 레이아웃 문제를 일으킬 수 있습니다. 특히 Type 3 연속 스크롤 시에는 전체 텍스트의 길이가 길어질 수 있습니다.
* **자동 업데이트:** 뉴스 바는 `newsPool/NewsPool.txt` 파일의 변경 사항을 주기적으로 확인하고 자동으로 표시를 업데이트합니다. (Type 3 스크롤 시에는 `--news-check-interval` 변수로 확인 간격 조절).

이 업데이트된 README는 OBS Real-time News Bar v0.41 버전을 사용하는 사용자들이 새로운 기능과 설정을 이해하고 효과적으로 사용자 정의하는 데 도움이 될 것입니다.
