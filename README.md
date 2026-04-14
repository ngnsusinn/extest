# ex_test.sty — Gói LaTeX soạn đề thi trắc nghiệm tiếng Việt

**Phiên bản gốc:** 2.4.3 (15/06/2018) — Trần Anh Tuấn  
**Phiên bản chỉnh sửa:** Nguyễn Sun Sin  

> **Phiên bản này đã được chỉnh sửa và bổ sung đáng kể bởi Nguyễn Sun Sin**, bao gồm các tính năng mới như **trắc nghiệm đúng/sai** (`\choiceTF`), **trả lời ngắn** (`\shortans`), **hệ thống bảng đáp án dạng lưới (Grid)**, **trộn đề từ nhiều nguồn (Mix Bank)**, **chế độ tiêu đề `\modede`**, và nhiều cải tiến khác. Xem mục [Tổng hợp các thay đổi](#-tổng-hợp-các-thay-đổi-bởi-nguyễn-sun-sin) và [Lịch sử chỉnh sửa](#lịch-sử-chỉnh-sửa) ở cuối tài liệu.

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Cài đặt](#cài-đặt)
- [Các gói phụ thuộc](#các-gói-phụ-thuộc)
- [Tùy chọn gói (Package Options)](#tùy-chọn-gói-package-options)
- [Môi trường (Environments)](#môi-trường-environments)
- [Lệnh soạn câu hỏi](#lệnh-soạn-câu-hỏi)
  - [Trắc nghiệm 4 phương án](#trắc-nghiệm-4-phương-án)
  - [Trắc nghiệm 5 phương án](#trắc-nghiệm-5-phương-án)
  - [Trắc nghiệm đúng/sai (MỚI)](#-trắc-nghiệm-đúngsai-mới)
  - [Trả lời ngắn (MỚI)](#-trả-lời-ngắn-mới)
- [Đánh dấu đáp án đúng](#đánh-dấu-đáp-án-đúng)
- [Lời giải](#lời-giải)
- [Chèn hình ảnh](#chèn-hình-ảnh)
- [Ngân hàng câu hỏi & Trộn đề](#ngân-hàng-câu-hỏi--trộn-đề)
  - [Mix Bank — Trộn từ nhiều nguồn (MỚI)](#-mix-bank--trộn-từ-nhiều-nguồn-mới)
- [Bảng đáp án dạng lưới Grid (MỚI)](#-bảng-đáp-án-dạng-lưới-grid-mới)
- [Tùy chỉnh tiêu đề đề thi](#tùy-chỉnh-tiêu-đề-đề-thi)
  - [Chế độ `\modede` (MỚI)](#-chế-độ-modede-mới)
- [Các lệnh tiện ích khác](#các-lệnh-tiện-ích-khác)
- [Ví dụ hoàn chỉnh](#ví-dụ-hoàn-chỉnh)
- [Tổng hợp các thay đổi bởi Nguyễn Sun Sin](#-tổng-hợp-các-thay-đổi-bởi-nguyễn-sun-sin)
- [Lịch sử chỉnh sửa](#lịch-sử-chỉnh-sửa)

---

## Giới thiệu

`ex_test` là gói LaTeX chuyên dụng để soạn đề thi trắc nghiệm bằng tiếng Việt. Gói hỗ trợ:

- Câu hỏi trắc nghiệm **4 hoặc 5 phương án** với bố cục tự động (1, 2, 4 cột).
- **[MỚI]** Câu hỏi **trắc nghiệm đúng/sai** (4 ý a, b, c, d) với lệnh `\choiceTF`.
- **[MỚI]** Câu hỏi **trả lời ngắn** (điền đáp án) với lệnh `\shortans`.
- Đánh dấu đáp án đúng, hiển thị/ẩn lời giải chi tiết.
- **Trộn đề thi** từ ngân hàng câu hỏi với đảo thứ tự phương án ngẫu nhiên.
- **[MỚI]** Trộn câu hỏi từ **nhiều nguồn khác nhau** (Mix Bank) với `\addtobank` + `\domixbank`.
- **[MỚI]** Xuất **bảng đáp án dạng lưới (Grid)** cho 3 loại câu hỏi: MC / TF / SA.
- **[MỚI]** Chế độ tiêu đề `\modede` — khung đơn giản cho đề cương/ôn tập.
- **[MỚI]** Lệnh `\showansfull` — hiển thị lời giải chi tiết theo mã đề.
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

Tương tự `ex`, dùng khi trộn đề bằng `\randombank`. Đáp án được ghi ra file `.xls`, `.tex` và **[MỚI]** file grid `ans/grid<mã đề>.tex`.

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

### ★ Trắc nghiệm đúng/sai (MỚI)

> **Tính năng mới** do Nguyễn Sun Sin bổ sung — hỗ trợ dạng câu hỏi đúng/sai theo chuẩn thi THPT Quốc gia.

#### `\choiceTF{a}{b}{c}{d}`

Tạo 4 mệnh đề a), b), c), d) — mỗi mệnh đề đúng hoặc sai. Đặt `\True` trước mệnh đề đúng. Bên trong gói, `\choiceTF` tự động:

- Đặt `\currentqtype` thành `TF` (thay vì `MC`).
- Theo dõi trạng thái đúng/sai qua 4 cờ `\tfAtrue`/`\tfAfalse` ... `\tfDtrue`/`\tfDfalse`.
- Khi dùng với `\randombank`, đáp án được ghi vào grid file dạng `ĐSĐS` (ví dụ: `D S D S`).

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

#### Tùy chỉnh nhãn `\choiceTFlabel`

```latex
\renewcommand{\choiceTFlabel}[1]{\textbf{#1)}}  % Mặc định: a) b) c) d)
```

### ★ Trả lời ngắn (MỚI)

> **Tính năng mới** do Nguyễn Sun Sin bổ sung — hỗ trợ dạng câu hỏi điền đáp số.

#### `\shortans{đáp án}`

Câu hỏi yêu cầu điền đáp số. Bên trong gói, `\shortans` tự động:

- Đặt `\currentqtype` thành `SA` (Short Answer).
- Lưu đáp án vào `\currentSAans` để ghi vào grid file.
- Gọi `\shortsol{đáp án}` để xuất đáp số vào file đáp án ngắn.

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

**[MỚI]** Trong `\choiceTF`, `\True` đánh dấu mệnh đề đúng (Đ), các mệnh đề không có `\True` là sai (S).

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

### ★ Mix Bank — Trộn từ nhiều nguồn (MỚI)

> **Tính năng mới** do Nguyễn Sun Sin bổ sung — cho phép trộn câu hỏi từ **nhiều file ngân hàng khác nhau** và xáo trộn thứ tự toàn bộ.

```latex
\resetmixbank                  % Khởi tạo / reset
\addtobank{chuong1.tex}{5}    % Lấy 5 câu ngẫu nhiên từ chương 1
\addtobank{chuong2.tex}{3}    % Lấy 3 câu ngẫu nhiên từ chương 2
\addtobank{chuong3.tex}{2}    % Lấy 2 câu ngẫu nhiên từ chương 3
\domixbank                     % Trộn ngẫu nhiên thứ tự và xuất 10 câu
```

| Lệnh                    | Mô tả                                                    |
| ------------------------ | --------------------------------------------------------- |
| `\resetmixbank`          | Xóa danh sách câu hỏi đã thêm, reset về trạng thái ban đầu |
| `\addtobank{file}{n}`    | Thêm `n` câu ngẫu nhiên từ `file` vào danh sách mix     |
| `\domixbank`             | Xáo trộn toàn bộ câu hỏi đã thêm và xuất dưới dạng `exrd` |

Cơ chế hoạt động:
1. `\addtobank` đọc file, đếm tổng số câu, chọn ngẫu nhiên `n` câu.
2. Lưu vị trí nguồn (file nào, câu thứ mấy) cho mỗi câu được chọn.
3. `\domixbank` tạo một danh sách thứ tự ngẫu nhiên, rồi lần lượt đọc và xuất từng câu.

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
5. **[MỚI]** Ghi file grid `ans/grid<mã đề>.tex` chứa đáp án cả 3 loại MC/TF/SA.
6. Đánh số trang riêng cho mỗi mã đề.

> **Lưu ý:** Cần tạo thư mục `ans/` trước khi biên dịch.

### `\choiceRD{A}{B}{C}{D}` / `\choicefiveRD{A}{B}{C}{D}{E}`

Phiên bản trộn ngẫu nhiên thứ tự phương án. Gói tự động chuyển sang dùng lệnh này khi gọi `\randombank`.

---

## ★ Bảng đáp án dạng lưới Grid (MỚI)

> **Tính năng mới hoàn toàn** do Nguyễn Sun Sin phát triển — thay thế bảng đáp án cũ bằng hệ thống Grid phân loại 3 dạng câu hỏi.

### Cơ chế hoạt động

Khi sử dụng `\randombank`, gói tự động ghi file `ans/grid<mã đề>.tex` chứa các lệnh `\gridcell{loại}{số câu}{đáp án}`:
- **MC** (Multiple Choice): `\gridcell{MC}{1}{A}` — câu 1, đáp án A.
- **TF** (True/False): `\gridcell{TF}{5}{DSDS}` — câu 5, Đúng-Sai-Đúng-Sai.
- **SA** (Short Answer): `\gridcell{SA}{8}{$7$}` — câu 8, đáp án $7$.

### `\showans{danh sách mã đề}`

Hiển thị bảng đáp án dạng lưới dùng `\forcsvlist` (thay vì `\foreach` cũ, tránh lỗi `\ifnum`). Bảng tự động chia thành 3 phần:

| Phần      | Số cột mặc định | Nội dung                                    |
| --------- | ---------------- | ------------------------------------------- |
| **Phần I**  | 12 cột           | Trắc nghiệm nhiều phương án (MC): số câu + đáp án A/B/C/D/E |
| **Phần II** | 4 cột            | Trắc nghiệm đúng/sai (TF): Câu N + pattern **Đ**/**S**      |
| **Phần III**| 6 cột            | Trắc nghiệm trả lời ngắn (SA): Câu N + đáp số               |

Mỗi phần chỉ hiển thị khi có câu hỏi thuộc loại đó.

```latex
\showans{101,102,103,104}
```

### `\showansfull{danh sách mã đề}`

> **Lệnh mới** — Hiển thị **lời giải chi tiết** cho từng mã đề.

```latex
\showansfull{101,102,103,104}
```

### Tùy chỉnh số cột và nhãn bảng Grid

```latex
% Số cột cho mỗi loại câu hỏi
\def\gridMCcolnum{12}   % Mặc định: 12 cột cho MC
\def\gridTFcolnum{4}    % Mặc định: 4 cột cho TF
\def\gridSAcolnum{6}    % Mặc định: 6 cột cho SA

% Nhãn tiêu đề từng phần
\def\gridlabelMC{PHẦN I. Trắc nghiệm nhiều phương án}
\def\gridlabelTF{PHẦN II. Trắc nghiệm đúng/sai}
\def\gridlabelSA{PHẦN III. Trắc nghiệm trả lời ngắn}
\def\showansheader{BẢNG ĐÁP ÁN CÁC MÃ ĐỀ}
```

### Các lệnh bảng đáp án kế thừa

| Lệnh                        | Mô tả                                           |
| ---------------------------- | ------------------------------------------------ |
| `\tabans{n}`                 | Đáp án dạng bảng `n` cột                        |
| `\rowans`                    | Đáp án dạng hàng ngang                           |
| `\boxans`                    | Đáp án trong ô viền                              |
| `\listans`                   | Đáp án dạng danh sách liên tục                   |
| `\inputans{n}{file}`         | Nhập đáp án từ file, hiển thị `n` cột           |
| `\inputansbox{n}{file}`      | Nhập đáp án từ file, hiển thị `n` cột có viền   |
| `\shortsolnum{n}`            | Đáp số câu tự luận, `n` cột                     |

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

### `\modedethi` — Tiêu đề đề thi chính thức

Bố cục 2 cột: bên trái tên sở/trường, bên phải tên kỳ thi + môn + thời gian. Dòng dưới có Họ tên, Số báo danh, Mã đề.

```latex
\modedethi
```

### ★ Chế độ `\modede` (MỚI)

> **Tính năng mới** do Nguyễn Sun Sin bổ sung — tiêu đề dạng khung đơn giản, phù hợp cho đề cương/ôn tập/bài tập.

```latex
\def\tieude{ĐỀ CƯƠNG ÔN TẬP TOÁN 12}
\def\phude{Năm học 2024 -- 2025}
\def\thoigian{90}
\modede
```

Kết quả: một khung viền chứa tiêu đề chữ lớn màu xanh, dòng thời gian in nghiêng, và phụ đề (nếu có).

### Chế độ hiển thị tiêu đề

| Lệnh           | Mô tả                                                                        |
| --------------- | ----------------------------------------------------------------------------- |
| `\modedethi`    | Tiêu đề đề thi chính thức (tên trường, kỳ thi, môn, thời gian, mã đề).     |
| `\modede`       | **[MỚI]** Tiêu đề dạng khung đơn giản (tiêu đề, phụ đề, thời gian).       |

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

### Ví dụ 1: Đề thi đơn giản (đầy đủ 3 dạng câu hỏi)

```latex
\documentclass[a4paper,12pt]{article}
\usepackage[loigiai]{ex_test}

\begin{document}

%% Câu trắc nghiệm nhiều phương án (MC)
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

%% Câu trắc nghiệm đúng/sai (TF) ★ MỚI
\begin{ex}
  Cho các mệnh đề sau về hàm số $f(x) = x^3$:
  \choiceTF
  {\True $f(0) = 0$}
  {$f(1) = 3$}
  {\True $f(-1) = -1$}
  {$f$ là hàm số chẵn}
\end{ex}

%% Câu trả lời ngắn (SA) ★ MỚI
\begin{ex}
  Tính $\displaystyle\int_0^1 2x\,dx = $ \shortans{$1$}
\end{ex}

\end{document}
```

### Ví dụ 2: Trộn đề từ nhiều nguồn (Mix Bank)

```latex
\documentclass[a4paper,12pt]{article}
\usepackage[dethi]{ex_test}

\def\tentruong{TRƯỜNG THPT ABC}
\def\tenkythi{KIỂM TRA GIỮA KỲ I}
\def\tenmonhoc{TOÁN 10}
\def\thoigian{60}
\modedethi

%% ★ MỚI: Dùng Mix Bank để trộn từ nhiều nguồn
\def\listfile{
  \resetmixbank
  \addtobank{dai_so.tex}{10}
  \addtobank{hinh_hoc.tex}{10}
  \addtobank{thong_ke.tex}{5}
  \addtobank{dung_sai.tex}{5}        % Chứa câu \choiceTF
  \addtobank{dien_dap_an.tex}{5}     % Chứa câu \shortans
  \domixbank
}

\begin{document}
\Opensolutionfile{ans}[ans/ans]

\randombank{101,102,103,104}

%% ★ MỚI: Bảng đáp án dạng Grid (MC + TF + SA)
\showans{101,102,103,104}

%% ★ MỚI: Lời giải chi tiết theo mã đề
\showansfull{101,102,103,104}

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
6. **[MỚI] Loại câu hỏi:** Mỗi câu `ex`/`exrd` mặc định là MC. Dùng `\choiceTF` sẽ chuyển thành TF, dùng `\shortans` sẽ chuyển thành SA.

---

## ★ Tổng hợp các thay đổi bởi Nguyễn Sun Sin

So với bản gốc v2.4.3 của Trần Anh Tuấn, phiên bản này có các thay đổi/bổ sung sau:

| #  | Thay đổi                                           | Mô tả chi tiết                                                                                             |
| -- | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| 1  | **`\choiceTF{a}{b}{c}{d}`**                         | Lệnh hoàn toàn mới — tạo câu hỏi trắc nghiệm đúng/sai gồm 4 mệnh đề a) b) c) d). Hỗ trợ `\True` đánh dấu mệnh đề đúng, theo dõi qua 4 cờ `\iftfA`..`\iftfD`. |
| 2  | **`\shortans{đáp án}`**                              | Lệnh hoàn toàn mới — câu hỏi trả lời ngắn (điền đáp số), tự động đặt `\currentqtype=SA` và ghi đáp án vào grid. |
| 3  | **Hệ thống theo dõi loại câu hỏi**                 | Thêm `\currentqtype` (MC/TF/SA), `\currentSAans`, 4 cờ boolean `\iftfA`..`\iftfD` để phân loại câu hỏi tự động. |
| 4  | **Hệ thống Grid file**                              | Thêm `\gridfile`, `\ifgridwriting`. `\randombank` tự động ghi `ans/grid<mã đề>.tex` chứa `\gridcell{loại}{câu}{đáp án}`. |
| 5  | **`\showans` viết lại hoàn toàn**                   | Dùng `\forcsvlist` thay `\foreach` (tránh lỗi `\ifnum`). Hiển thị bảng lưới tabular cho MC (12 cột), TF (4 cột), SA (6 cột). |
| 6  | **Grid renderers**                                   | Bộ lệnh mới: `\gridcell`, `\gridMCitem`, `\gridTFitem`, `\gridSAitem`, `\displayDSpattern`, `\gridcheckrow`, `\gridpadloop`, và các `padend`. |
| 7  | **Tùy chỉnh Grid**                                  | Biến mới: `\gridMCcolnum`, `\gridTFcolnum`, `\gridSAcolnum`, `\gridlabelMC`, `\gridlabelTF`, `\gridlabelSA`, `\showansheader`. |
| 8  | **Mix Bank (`\addtobank`, `\domixbank`)**            | Hệ thống hoàn toàn mới — lấy câu hỏi từ nhiều file nguồn, lưu trữ source/question index, trộn thứ tự rồi xuất. |
| 9  | **`\showansfull{mã đề}`**                            | Lệnh mới — hiển thị lời giải chi tiết cho từng mã đề từ file `ans/ansrd<mã đề>.tex`. |
| 10 | **`\modede`**                                        | Chế độ tiêu đề mới — khung viền đơn giản với `\tieude`, `\phude`, `\thoigian`. Bổ sung biến `\tieude`, `\phude`. |
| 11 | **Grid ghi đáp án TF/SA trong `\AtEndEnvironment`** | `\AtEndEnvironment{ex}` và `\AtEndEnvironment{exrd}` được mở rộng: ngoài MC, còn ghi đáp án TF (pattern ĐSĐS) và SA vào grid file. |
| 12 | **`\choiceTFlabel` có thể tùy chỉnh**               | Nhãn mệnh đề TF (mặc định `\textbf{#1)}`) có thể renew. |
| 13 | **`\randombank` mở rộng**                           | Thêm mở/đóng `\gridfile`, `\gridwritingtrue`/`false`, và lưu/khôi phục `\choicefive` → `\choicefiveRD`. |

---

## Lịch sử chỉnh sửa

### v2.4.3 — 15/06/2018 (Trần Anh Tuấn)

- Phiên bản gốc phát hành.
- Hỗ trợ câu hỏi trắc nghiệm 4 phương án (`\choice`) và 5 phương án (`\choicefive`).
- Tự động bố cục 1/2/4 cột và 5 cách bố cục cho 5 phương án.
- Trộn đề `\randombank` với `\choiceRD` / `\choicefiveRD` (đảo 24 hoán vị cho 4 PA, 120 cho 5 PA).
- Ngân hàng câu hỏi `\bankEX`.
- Các option: `dethi`, `color`, `solcolor`, `loigiai`, `book`, `circle`, `twocol`.
- Lời giải `\loigiai`, ẩn/hiện với `\showansEX` / `\hideansEX`.
- Chèn hình: `\immini`, `\impicinpar`.
- TikZ: `\Interval*`, `\trucLG`, `\pointLG`.
- Bảng đáp án: `\tabans`, `\rowans`, `\boxans`, `\listans`, `\inputans`.
- Tiêu đề đề thi: `\modedethi`.

### Bản chỉnh sửa — Nguyễn Sun Sin

- **Thêm `\choiceTF`**: Dạng câu hỏi trắc nghiệm đúng/sai (4 mệnh đề a-d), theo chuẩn thi THPT. Bao gồm `\choiceTFlabel`, counter `tfitem`, 4 cờ boolean `\iftfA`..`\iftfD`.
- **Thêm `\shortans`**: Dạng câu hỏi trả lời ngắn, tự động theo dõi loại SA.
- **Thêm hệ thống phân loại câu hỏi**: `\currentqtype` (MC/TF/SA), `\currentSAans` — tự động nhận diện loại câu.
- **Thêm hệ thống Grid**: Ghi file `\gridfile` khi trộn đề, parser `\gridcell`, renderers `\gridMCitem`/`\gridTFitem`/`\gridSAitem`. Bảng đáp án dạng lưới tabular chia 3 phần MC/TF/SA.
- **Viết lại `\showans`**: Dùng `\forcsvlist` thay `\foreach` để tránh lỗi nested `\ifnum`. Tích hợp hiển thị Grid cho cả 3 loại câu hỏi.
- **Thêm biến tùy chỉnh Grid**: `\gridMCcolnum`, `\gridTFcolnum`, `\gridSAcolnum`, `\gridlabelMC`, `\gridlabelTF`, `\gridlabelSA`, `\showansheader`.
- **Thêm Mix Bank**: `\resetmixbank`, `\addtobank{file}{n}`, `\domixbank` — trộn câu hỏi từ nhiều nguồn.
- **Thêm `\showansfull`**: Hiển thị lời giải chi tiết theo mã đề.
- **Thêm `\modede`**: Chế độ tiêu đề khung viền đơn giản. Thêm biến `\tieude`, `\phude`.
- **Mở rộng `\randombank`**: Tích hợp ghi grid file, lưu/khôi phục `\choicefive` ↔ `\choicefiveRD`.
- **Mở rộng `\AtEndEnvironment{ex}` và `{exrd}`**: Ghi đáp án TF (pattern Đ/S) và SA vào grid file ngoài MC.

---

## Giấy phép

Gói `ex_test` được phát triển ban đầu bởi **Trần Anh Tuấn** (2018).  
Phiên bản chỉnh sửa và bổ sung bởi **Nguyễn Sun Sin**.
