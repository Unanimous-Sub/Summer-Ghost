# SubKt Project template

## Phần mềm cần thiết

- [mkvmerge](https://mkvtoolnix.download/downloads.html)
- [JDK 16](https://www.oracle.com/java/technologies/javase/jdk16-archive-downloads.html)

## Cấu trúc thư mục
Các tệp tin sau đây sẽ cần được điều chỉnh tuỳ vào các project khác nhau.  
VD: Tên của bộ sẽ làm `New Show` và tên rút gọn là `New`.

- **Thư mục gốc:**

  - `build.gradle.kts`: SubKt Gradle build script.
  - `sub.properties`: Tệp cấu hình các thuộc tính của project.

- **01/**: Ví dụ thư mục của một tập phim.

  - `New 01 - Dialogue.ass`: Chứa phụ đề cho phần hội thoại.
  - `New 01 - TS.ass`: Chứa phụ đề cho phần Typeset.
    - Có thể có nhiều tập tin TS.  
    - Ví dụ: `New 01 - TS (rainei).ass` & `New 01 - TS (moca).ass`
  - `New 01 - INS.ass` (Tuỳ chọn): Chứa phụ đề cho phần nhạc insert.
    - Có thể có nhiều tập tin INS.  
    - Ví dụ: `New 01 - INS (OP).ass` & `New 01 - INS (Tên Nhạc).ass`
  - `New 01 - Extra.ass` (Tuỳ chọn): Chứa phụ đề bổ sung, khi chúng không phù hợp để cho vào các trường hợp ở trên.
	
- **NCOP{x}/NCED{x}** (Tuỳ chọn):
	- `New_NCOP{x}.ass/New_NCED{x}.ass`: Chứa phụ đề cho OP{x}/ED{x}.
	
- `fonts/`: Thư mục chứa font của toàn bộ project.
- `raws/`: Thư mục chứa raw của toàn bộ project.

## Bắt đầu

Để bắt đầu sử dụng template này:

1. **Sử dụng Template:**

   Nhấp vào nút sau đây ở phía trên bên phải của repo GitHub.

   ![Github "Use this template" button](https://i.imgur.com/zT0SLVM.png)

2. **Thiết lập project:**

   Thông thường thì một project cơ bản, sẽ cần điều chỉnh các tập tin sau đây:

   - Tập tin `sub.properties`.
     - Đặt tên nhóm và tên của bộ dự định làm.
     - Đặt dịnh dạng của video và audio dựa trên raw sử dụng.
     - Đặt số tập. 
      - VD: `episodes={01..24}` — Có nghĩa là số tập được đặt là từ 01 đến 24.
     - Đặt OP, ED cho các tập. 
      - VD: `{02..06}|{08..12}.OP_name=NCOP1` — Có nghĩa là OP1 sẽ có từ tập 02 đến 06 và từ 08 đến 12.
	 - Điều chỉnh `raws` phù hợp với cấu trúc tên của raw.
   - Thêm hội thoại và chapter vào file `Dialouge` của tập. Chapter được đánh dấu bằng dòng phụ đề có trường Actor là `chapter`, điểm bắt đầu là frame đầu tiên của chapter tương ứng, nội dung của dòng này là tên của chapter.
     - VD: `Comment: 0,0:00:00.00,0:00:00.02,[16:9] Main,chapter,0,0,0,,{Prologue}` — Có nghĩa là chapter bắt đầu từ 0:00:00, và có tên là **Prologue**.
   - Thêm Typeset vào tệp phụ đề TS của tập.
   - Thêm phụ đề INS và Extra (Tuỳ chọn).
   - Thu thập toàn bộ font sử dụng trong project và đặt vào thư mục `fonts/`.
   - Đối với phụ đề OP và ED.
     - Sử dụng video chỉ có OP hoặc ED được cắt ra từ tập nào đó đối với TVs, nếu là BD thì hãy sử dụng NCOP và NCED.
	   - Ở file `Dialogue`, thêm một dòng phụ đề có trường Effect là `opsync` đối với OP, `edsync` đối với ED. Đối với tập tin OP và ED, thêm dòng phụ có trường Effect là `sync`. Điểm bắt đầu của 2 dòng này sẽ là frame đầu tiên của OP hoặc ED. 2 điểm này sẽ được sử dụng để sync và merge OP vào ED vào các tập khác nhau.

3. **Build project:**

   Sử dụng Gradle wrapper để build project:

   ```sh
   ./gradlew mux.01   # Đối với Unix
   gradlew.bat mux.01 # Đối với Windows
   ```

   `mux` có thể được thay thế bằng bất kì lệnh nào sau đây:

   - `chapters`: Tạo chapter từ tệp phụ đề hội thoại.
   - `merge`: Merge phụ đề của tập lại, cũng như các tệp phụ đề OP và ED.
   
   ```sh
   ./gradlew -q :tasks --all   # Đối với Unix
   gradlew.bat -q :tasks --all # Đối với Windows
   ```
   <!-- Để xem toàn bộ tasks. -->
