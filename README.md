# ex_test.sty — Gói LaTeX soạn đề thi trắc nghiệm tiếng Việt

**Phiên bản:** 2.4.3  
**Ngày phát hành:** 15/06/2018  
**Tác giả:** Trần Anh Tuấn

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Cài đặt](#cài-đặt)
- [Các gói phụ thuộc](#các-gói-phụ-thuộc)
- [Tùy chọn gói (Package Options)](#tùy-chọn-gói-package-options)
- [Môi trường (Environments)](#môi-trường-environments)
- [Lệnh soạn câu hỏi](#lệnh-soạn-câu-hỏi)
  - [Trắc nghiệm 4 phương án](#trắc-nghiệm-4-phương-án)
  - [Trắc nghiệm 5 phương án](#trắc-nghiệm-5-phương-án)
  - [Trắc nghiệm đúng/sai](#trắc-nghiệm-đúngsai)
  - [Trả lời ngắn](#trả-lời-ngắn)
- [Đánh dấu đáp án đúng](#đánh-dấu-đáp-án-đúng)
- [Lời giải](#lời-giải)
- [Chèn hình ảnh](#chèn-hình-ảnh)
- [Ngân hàng câu hỏi & Trộn đề](#ngân-hàng-câu-hỏi--trộn-đề)
- [Bảng đáp án](#bảng-đáp-án)
- [Tùy chỉnh tiêu đề đề thi](#tùy-chỉnh-tiêu-đề-đề-thi)
- [Các lệnh tiện ích khác](#các-lệnh-tiện-ích-khác)
- [Ví dụ hoàn chỉnh](#ví-dụ-hoàn-chỉnh)

---

## Giới thiệu

`ex_test` là gói LaTeX chuyên dụng để soạn đề thi trắc nghiệm bằng tiếng Việt. Gói hỗ trợ:

- Câu hỏi trắc nghiệm **4 hoặc 5 phương án** với bố cục tự động (1, 2, 4 cột).
- Câu hỏi **trắc nghiệm đúng/sai** (4 ý a, b, c, d).
- Câu hỏi **trả lời ngắn** (điền đáp án).
- Đánh dấu đáp án đúng, hiển thị/ẩn lời giải chi tiết.
- **Trộn đề thi** từ ngân hàng câu hỏi với đảo thứ tự phương án ngẫu nhiên.
- Xuất **bảng đáp án** dạng lưới (grid) cho nhiều mã đề.
- Hỗ trợ chèn hình ảnh bên cạnh văn bản.
- Vẽ **khoảng/đoạn trên trục số** và **đường tròn lượng giác** bằng TikZ.

---

## Cài đặt

Sao chép file `ex_test.sty` vào cùng thư mục với file `.tex` của bạn, hoặc đặt vào thư mục `texmf` local.

```latex
\usepackage{ex_test}
```

---

## Các gói phụ thuộc

Gói tự động nạp các gói sau (không cần `\usepackage` thêm):

| Gói            | Mục đích                            |
| -------------- | ----------------------------------- |
| `ifthen`       | Điều kiện logic                     |
| `fancyhdr`     | Tùy chỉnh header/footer            |
| `multicol`     | Bố cục nhiều cột                    |
| `answers`      | Quản lý đáp án                      |
| `array`        | Mở rộng bảng                        |
| `multirow`     | Ô gộp hàng trong bảng              |
| `longtable`    | Bảng dài nhiều trang                |
| `vietnam`      | Hỗ trợ tiếng Việt (UTF-8)          |
| `tikz`         | Vẽ hình                             |
| `ntheorem`     | Định lý/môi trường đánh số         |
| `calc`         | Tính toán chiều dài                 |
| `etoolbox`     | Công cụ lập trình LaTeX            |
| `probsoln`     | Quản lý bài toán & lời giải        |
| `picinpar`     | Chèn hình trong đoạn văn           |
| `catchfile`    | Đọc file vào macro                  |
| `environ`      | Thu thập nội dung môi trường       |
| `amsmath`      | Công thức toán học                  |
| `filecontents` | Ghi nội dung ra file                |
| `paralist`     | Danh sách trong dòng                |
| `tabto`        | Tab stop                            |

---

## Tùy chọn gói (Package Options)

```latex
\usepackage[<option>]{ex_test}
```

| Tùy chọn    | Mô tả                                                                                  |
| ------------ | --------------------------------------------------------------------------------------- |
| `dethi`      | **(mặc định)** Chế độ đề thi — ẩn đáp án đúng, ẩn lời giải, ẩn nội dung ô `\boxEX`. |
| `color`      | Tô màu đỏ đáp án đúng (khung vuông), đáp án sai (khung tròn).                         |
| `solcolor`   | Như `color` + hiển thị lời giải chi tiết.                                               |
| `loigiai`    | Hiển thị lời giải chi tiết, các phương án hiển thị dạng chữ (A. B. C. D.).             |
| `book`       | Chế độ sách — ghi lời giải vào file riêng bằng `\solbook`.                             |
| `circle`     | Hiển thị đáp án dạng khoanh tròn (○A ○B ○C ○D).                                       |
| `twocol`     | Bố cục hai cột cho toàn bộ nội dung.                                                   |

Có thể kết hợp nhiều tùy chọn:

```latex
\usepackage[solcolor,twocol]{ex_test}
```

---

## Môi trường (Environments)

### `ex` — Câu hỏi thi

Môi trường chính để soạn câu hỏi. Tự động đánh số "Câu 1.", "Câu 2.", ...

```latex
\begin{ex}
  Phương trình $x^2 - 5x + 6 = 0$ có hai nghiệm là
  \choice
  {\True $x=2$ và $x=3$}
  {$x=1$ và $x=6$}
  {$x=-2$ và $x=-3$}
  {$x=0$ và $x=5$}
  \loigiai{
    Ta có $\Delta = 25 - 24 = 1$. Suy ra $x = 2$ hoặc $x = 3$.
  }
\end{ex}
```

### `exrd` — Câu hỏi cho trộn đề

Tương tự `ex`, dùng khi trộn đề bằng `\randombank`. Đáp án được ghi ra file `.xls` và `.tex`.

### `vdex` — Ví dụ

Đánh số "Ví dụ 1.", "Ví dụ 2.", ... Dùng để soạn ví dụ minh họa.

```latex
\begin{vdex}
  Tính $\int_0^1 x^2\,dx$.
  \loigiai{...}
\end{vdex}
```

### `listEX[n]` — Danh sách nhiều cột

Liệt kê dạng a) b) c) ... có thể chia thành `n` cột.

```latex
\begin{listEX}[3]  % 3 cột
  \item $x = 1$
  \item $x = 2$
  \item $x = 3$
  \item $x = 4$
  \item $x = 5$
  \item $x = 6$
\end{listEX}
```

Nếu bỏ tham số `[n]` hoặc dùng `[1]`, danh sách hiển thị 1 cột.

### `enumEX[label]{n}` — Danh sách đánh số với cột

```latex
\begin{enumEX}[a)]{2}  % nhãn a), chia 2 cột
  \item Nội dung 1
  \item Nội dung 2
  \item Nội dung 3
  \item Nội dung 4
\end{enumEX}
```

---

## Lệnh soạn câu hỏi

### Trắc nghiệm 4 phương án

#### `\choice{A}{B}{C}{D}` — Tự động bố cục

Tự động chọn bố cục phù hợp dựa trên độ rộng nội dung:
- **4 cột** (`\boncot`) nếu phương án ngắn.
- **2 cột** (`\haicot`) nếu phương án vừa.
- **1 cột** (`\motcot`) nếu phương án dài.

```latex
\begin{ex}
  Giá trị của $2 + 3$ bằng
  \choice{$4$}{\True $5$}{$6$}{$7$}
\end{ex}
```

#### Bố cục thủ công

| Lệnh              | Bố cục             |
| ------------------ | ------------------- |
| `\boncot{A}{B}{C}{D}` | 4 phương án trên 1 hàng |
| `\haicot{A}{B}{C}{D}` | 2 phương án mỗi hàng    |
| `\motcot{A}{B}{C}{D}` | 1 phương án mỗi hàng    |

#### `\choicew{length}` — Đặt chiều rộng tối thiểu

Ép `\choice` dùng bố cục dựa trên chiều rộng tùy chỉnh:

```latex
\choicew{5cm}
\choice{...}{...}{...}{...}
```

#### `\choicefix{A}{B}{C}{D}`

Tương tự `\choice` nhưng không reset chiều rộng từ lần gọi `\choicew` trước.

### Trắc nghiệm 5 phương án

#### `\choicefive{A}{B}{C}{D}{E}` — Tự động bố cục

Tự phân bố 5 phương án với các layout:
- **5 trên 1 hàng** (`\nammot`)
- **3 + 2** (`\bahai`) — hàng 1: 3 phương án, hàng 2: 2 phương án
- **2 + 3** (`\haiba`) — hàng 1: 2 phương án, hàng 2: 3 phương án
- **1 cột** (`\motnam`) — mỗi phương án một hàng

```latex
\begin{ex}
  Tập xác định của hàm số $y = \sqrt{x}$ là
  \choicefive
  {$\mathbb{R}$}
  {\True $[0;+\infty)$}
  {$(0;+\infty)$}
  {$(-\infty;0]$}
  {$(-\infty;0)$}
\end{ex}
```

### Trắc nghiệm đúng/sai

#### `\choiceTF{a}{b}{c}{d}`

Tạo 4 mệnh đề a), b), c), d) — mỗi mệnh đề đúng hoặc sai.

```latex
\begin{ex}
  Cho hàm số $f(x) = x^2$. Các mệnh đề sau đúng hay sai?
  \choiceTF
  {\True $f(0) = 0$}
  {$f(1) = 2$}
  {\True $f(-1) = 1$}
  {$f(2) = 5$}
\end{ex}
```

Đặt `\True` trước mệnh đề đúng. Đáp án xuất ra dạng `Đ`/`S` (Đúng/Sai).

### Trả lời ngắn

#### `\shortans{đáp án}`

Câu hỏi yêu cầu điền đáp số.

```latex
\begin{ex}
  Tính $3 + 4 = $ \shortans{$7$}
\end{ex}
```

---

## Đánh dấu đáp án đúng

### `\True`

Đặt **trước** nội dung phương án đúng trong `\choice`, `\choicefive`, hoặc `\choiceTF`.

```latex
\choice
{$x = 1$}
{\True $x = 2$}   % Đáp án B là đáp án đúng
{$x = 3$}
{$x = 4$}
```

Tùy theo option của gói:
- `dethi`: Không hiển thị sự khác biệt.
- `color` / `solcolor`: Đáp án đúng tô màu đỏ, viền vuông; đáp án sai viền tròn.

---

## Lời giải

### `\loigiai{nội dung}`

Chèn lời giải chi tiết vào câu hỏi. Hiển thị hoặc ẩn tùy theo option.

```latex
\begin{ex}
  Tính $\lim_{x \to 0} \dfrac{\sin x}{x}$.
  \choice{\True $1$}{$0$}{$+\infty$}{Không tồn tại}
  \loigiai{
    Áp dụng giới hạn cơ bản: $\lim_{x \to 0} \dfrac{\sin x}{x} = 1$.
  }
\end{ex}
```

### Lệnh chọn đáp án trong lời giải

Trong option `solcolor` và `loigiai`, cuối lời giải tự động hiển thị dòng "Chọn đáp án **X**" tương ứng đáp án đúng.

- `\hidetextchoice` — Ẩn dòng "Chọn đáp án".
- `\showtextchoice` — Hiện lại dòng "Chọn đáp án".

### `\showansEX{env}` / `\hideansEX{env}`

Bật/tắt hiển thị lời giải cho một môi trường cụ thể:

```latex
\showansEX{ex}   % Hiện lời giải trong môi trường ex
\hideansEX{ex}   % Ẩn lời giải trong môi trường ex
```

### `\dotlineans{n}{env}`

Thay lời giải bằng `n` dòng kẻ chấm (để học sinh tự viết) trong môi trường `env`:

```latex
\dotlineans{5}{ex}  % 5 dòng chấm thay cho lời giải
```

---

## Chèn hình ảnh

### `\immini[khoảng cách]{văn bản}{hình ảnh}`

Đặt hình ảnh bên phải, văn bản bên trái. Tham số tùy chọn `[khoảng cách]` là tỷ lệ khoảng trống giữa hai phần (0 = sát nhau).

```latex
\begin{ex}
  \immini[0.02]{
    Cho hình vẽ bên. Tính diện tích hình tròn.
    \choice{\True $\pi r^2$}{$2\pi r$}{$\pi r$}{$4\pi r^2$}
  }{
    \includegraphics[width=3cm]{hinh.png}
  }
\end{ex}
```

### `\impicinpar{văn bản}{hình ảnh}`

Chèn hình ảnh bên phải với text wrap (dùng gói `picinpar`).

```latex
\begin{ex}
  \impicinpar{
    Cho hình vẽ bên, tính chu vi...
    \choice{...}{...}{...}{...}
  }{
    \includegraphics[width=3cm]{hinh.png}
  }
\end{ex}
```

---

## Ngân hàng câu hỏi & Trộn đề

### `\bankEX{file}{n}`

Lấy ngẫu nhiên `n` câu hỏi từ file ngân hàng `file`.

```latex
\bankEX{ngan_hang.tex}{10}  % Lấy 10 câu ngẫu nhiên từ ngan_hang.tex
```

### Trộn từ nhiều nguồn (Mix Bank)

```latex
\resetmixbank
\addtobank{chuong1.tex}{5}   % 5 câu từ chương 1
\addtobank{chuong2.tex}{3}   % 3 câu từ chương 2
\addtobank{chuong3.tex}{2}   % 2 câu từ chương 3
\domixbank                    % Trộn và xuất 10 câu
```

### `\randombank{danh sách mã đề}`

Tạo nhiều mã đề thi khác nhau từ ngân hàng câu hỏi. Mỗi mã đề có thứ tự câu hỏi và phương án được trộn ngẫu nhiên.

```latex
\def\listfile{
  \bankEX{ngan_hang.tex}{30}
}
\randombank{101,102,103,104}
```

Lệnh này tự động:
1. Tạo mỗi mã đề trên trang mới.
2. Trộn ngẫu nhiên thứ tự câu hỏi.
3. Đảo thứ tự phương án (dùng `\choiceRD` thay `\choice`).
4. Ghi đáp án ra thư mục `ans/` (file `.xls`, `.tex`).
5. Đánh số trang riêng cho mỗi mã đề.

> **Lưu ý:** Cần tạo thư mục `ans/` trước khi biên dịch.

### `\choiceRD{A}{B}{C}{D}` / `\choicefiveRD{A}{B}{C}{D}{E}`

Phiên bản trộn ngẫu nhiên thứ tự phương án. Gói tự động chuyển sang dùng lệnh này khi gọi `\randombank`.

---

## Bảng đáp án

### `\showans{danh sách mã đề}`

Hiển thị bảng đáp án dạng lưới cho các mã đề. Bảng chia thành 3 phần:
- **Phần I** — Trắc nghiệm nhiều phương án (12 cột).
- **Phần II** — Trắc nghiệm đúng/sai (4 cột, hiển thị Đ/S).
- **Phần III** — Trắc nghiệm trả lời ngắn (6 cột).

```latex
\showans{101,102,103,104}
```

### `\showansfull{danh sách mã đề}`

Hiển thị **lời giải chi tiết** cho từng mã đề.

```latex
\showansfull{101,102,103,104}
```

### Tùy chỉnh bảng đáp án

| Lệnh                        | Mô tả                                           |
| ---------------------------- | ------------------------------------------------ |
| `\tabans{n}`                 | Đáp án dạng bảng `n` cột                        |
| `\rowans`                    | Đáp án dạng hàng ngang                           |
| `\boxans`                    | Đáp án trong ô viền                              |
| `\listans`                   | Đáp án dạng danh sách liên tục                   |
| `\inputans{n}{file}`         | Nhập đáp án từ file, hiển thị `n` cột           |
| `\inputansbox{n}{file}`      | Nhập đáp án từ file, hiển thị `n` cột có viền   |
| `\shortsolnum{n}`            | Đáp số câu tự luận, `n` cột                     |

### Tùy chỉnh nhãn bảng đáp án

```latex
\def\gridlabelMC{PHẦN I. Trắc nghiệm nhiều phương án}
\def\gridlabelTF{PHẦN II. Trắc nghiệm đúng/sai}
\def\gridlabelSA{PHẦN III. Trắc nghiệm trả lời ngắn}
\def\showansheader{BẢNG ĐÁP ÁN CÁC MÃ ĐỀ}
```

---

## Tùy chỉnh tiêu đề đề thi

### Biến tiêu đề

```latex
\def\tentruong{TRƯỜNG THPT ABC}
\def\tenso{SỞ GD\&ĐT XYZ}
\def\tenkythi{KIỂM TRA CUỐI KỲ II}
\def\tenmonhoc{TOÁN 12}
\def\thoigian{90}                    % phút
\def\sotrang{4}                      % số trang đề thi
```

Cho chế độ `\modede`:

```latex
\def\tieude{ĐỀ CƯƠNG ÔN TẬP TOÁN 12}
\def\phude{Năm học 2024 -- 2025}
```

### Chế độ hiển thị tiêu đề

| Lệnh           | Mô tả                                                                        |
| --------------- | ----------------------------------------------------------------------------- |
| `\modedethi`    | Tiêu đề đề thi chính thức (tên trường, kỳ thi, môn, thời gian, mã đề).     |
| `\modede`       | Tiêu đề dạng khung đơn giản (tiêu đề, phụ đề, thời gian).                  |

```latex
\modedethi   % Sau đó gọi \randombank{...}
```

---

## Các lệnh tiện ích khác

### Ẩn/hiện công thức

| Lệnh          | Mô tả                                                                  |
| -------------- | ----------------------------------------------------------------------- |
| `\sh{text}`    | Chế độ `dethi`: thay `text` bằng đường kẻ cùng kích thước. Các chế độ khác: hiện `text`. |
| `\boxEX[size]{content}` | Ô vuông. Chế độ `dethi`: ô rỗng. Các chế độ khác: hiện `content`. |
| `\TF{content}` | Ô vuông cho đúng/sai. Chế độ `dethi`: ô rỗng.                        |

### Gán nhãn công thức

```latex
\tagEX{1}   % Gán nhãn (1) bên phải, canh phải
```

### Dòng kẻ chấm

```latex
\dotlineEX{5}   % In 5 dòng kẻ chấm
```

### Đáp số ngắn (tự luận)

```latex
\shortsol{đáp số}
```

### Kí hiệu QED

```latex
\qedEX   % In ký hiệu □ kết thúc chứng minh
```

### Trích dẫn nguồn câu hỏi

Dùng theorem style `explain` để ghi nguồn trích dẫn câu hỏi:

```latex
\listtheorem{ex,vdex}   % Kích hoạt trích dẫn cho môi trường ex và vdex
```

### Tùy chỉnh tên câu hỏi

```latex
\renewcommand{\nameex}{Question}   % Đổi "Câu" thành "Question"
```

### Tùy chỉnh dấu kết thúc phương án

```latex
\def\dotEX{;}   % Đổi dấu chấm thành dấu chấm phẩy sau phương án
```

---

## Biểu diễn khoảng trên trục số (TikZ)

Các lệnh vẽ khoảng, đoạn trên trục số trong môi trường `tikzpicture`:

| Lệnh                                  | Mô tả                                    |
| -------------------------------------- | ----------------------------------------- |
| `\Interval{ký hiệu trái}{x1}{ký hiệu phải}{x2}` | Gạch chéo (ticks) trên đoạn |
| `\IntervalR{...}`                      | Gạch nghiêng phải (//)                    |
| `\IntervalL{...}`                      | Gạch nghiêng trái (\\\\)                  |
| `\IntervalLF{...}`                     | Tô gạch chéo trái (pattern fill)         |
| `\IntervalRF{...}`                     | Tô gạch chéo phải (pattern fill)         |
| `\IntervalLR{a}{b}`                    | Đặt tọa độ trái/phải cho lệnh `G`       |
| `\IntervalG{...}`                      | Như `\Interval`, dùng tọa độ từ `\IntervalLR` |

```latex
\begin{tikzpicture}
  \draw[->] (-3,0) -- (3,0);
  \Interval{[}{-2}{]}{2}
\end{tikzpicture}
```

---

## Đường tròn lượng giác (TikZ)

```latex
\begin{tikzpicture}
  \trucLG               % Vẽ trục và đường tròn đơn vị
  \pointLG{30}{12}{*}{red}  % Vẽ 12 điểm, bắt đầu từ 30°, dấu *, màu đỏ
\end{tikzpicture}
```

| Lệnh                              | Mô tả                                      |
| ---------------------------------- | ------------------------------------------- |
| `\trucLG`                          | Vẽ trục tọa độ + đường tròn đơn vị         |
| `\pointLG{góc}{số điểm}{mark}{màu}` | Vẽ các điểm trên đường tròn              |

---

## Ví dụ hoàn chỉnh

### Ví dụ 1: Đề thi đơn giản

```latex
\documentclass[a4paper,12pt]{article}
\usepackage[loigiai]{ex_test}

\begin{document}

\begin{ex}
  Tập nghiệm của phương trình $x^2 = 4$ là
  \choice
  {$\{2\}$}
  {\True $\{-2; 2\}$}
  {$\{-2\}$}
  {$\{4\}$}
  \loigiai{
    $x^2 = 4 \Leftrightarrow x = \pm 2$.
  }
\end{ex}

\begin{ex}
  Cho các mệnh đề sau về hàm số $f(x) = x^3$:
  \choiceTF
  {\True $f(0) = 0$}
  {$f(1) = 3$}
  {\True $f(-1) = -1$}
  {$f$ là hàm số chẵn}
\end{ex}

\begin{ex}
  Tính $\displaystyle\int_0^1 2x\,dx = $ \shortans{$1$}
\end{ex}

\end{document}
```

### Ví dụ 2: Trộn đề thi từ ngân hàng

**File `ngan_hang.tex`:**

```latex
\begin{ex}
  Câu hỏi 1...
  \choice{\True Đáp án đúng}{Sai 1}{Sai 2}{Sai 3}
\end{ex}

\begin{ex}
  Câu hỏi 2...
  \choice{Sai 1}{\True Đáp án đúng}{Sai 2}{Sai 3}
\end{ex}
% ... thêm nhiều câu hỏi
```

**File chính:**

```latex
\documentclass[a4paper,12pt]{article}
\usepackage[dethi]{ex_test}

\def\tentruong{TRƯỜNG THPT ABC}
\def\tenkythi{KIỂM TRA GIỮA KỲ I}
\def\tenmonhoc{TOÁN 10}
\def\thoigian{60}
\modedethi

\def\listfile{
  \bankEX{ngan_hang.tex}{20}
}

\begin{document}
\Opensolutionfile{ans}[ans/ans]

\randombank{101,102,103,104}

\showans{101,102,103,104}

\Closesolutionfile{ans}
\end{document}
```

> **Lưu ý:** Tạo thư mục `ans/` trước khi biên dịch. Biên dịch **2 lần** để đáp án hiển thị đúng.

### Ví dụ 3: Kết hợp hình ảnh

```latex
\begin{ex}
  \immini[0.02]{
    Cho hình chóp $S.ABC$ như hình vẽ bên.
    Tính thể tích khối chóp.
    \choice
    {\True $\dfrac{a^3}{6}$}
    {$\dfrac{a^3}{3}$}
    {$\dfrac{a^3}{2}$}
    {$a^3$}
    \loigiai{
      $V = \dfrac{1}{3} \cdot S_{ABC} \cdot h = \dfrac{a^3}{6}$.
    }
  }{
    \begin{tikzpicture}[scale=1.2]
      % Vẽ hình chóp
      \draw (0,0) node[below]{$A$} -- (2,0) node[below]{$B$}
            -- (1,0.8) node[right]{$C$} -- cycle;
      \draw (1,2.5) node[above]{$S$} -- (0,0);
      \draw (1,2.5) -- (2,0);
      \draw[dashed] (1,2.5) -- (1,0.8);
    \end{tikzpicture}
  }
\end{ex}
```

---

## Lưu ý quan trọng

1. **Mã hóa file:** Sử dụng UTF-8 (gói `vietnam` tự xử lý).
2. **Biên dịch:** Dùng `pdflatex` (2 lần cho đáp án đầy đủ).
3. **Thư mục `ans/`:** Phải tạo trước khi dùng `\randombank` hoặc `\showans`.
4. **`\True` luôn đặt trước nội dung** phương án đúng, không đặt sau.
5. **Trộn đề:** `\randombank` tự động thay `\choice` → `\choiceRD` và `\loigiai` → `\loigiaiRD`.

---

## Giấy phép

Gói `ex_test` được phát triển bởi **Trần Anh Tuấn** (2018).
