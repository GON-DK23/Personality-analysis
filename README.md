# Các yếu tố ảnh hưởng đến phân loại người hướng ngoại, hướng nội
--
## Mục lục
* [1. Giới thiệu](##-Giới-thiệu)
* [2. Tiền xử lý dữ liệu](##-Tiền-xử-lý-dữ-liệu)
  * [2.1. Đọc và kiểm tra dữ liệu](###-Đọc-và-kiểm-tra-dữ-liệu)
  * [2.2. Kiểm tra và xử lý ngoại lai]
* [3. Phân tích thành phần chính - PCA]
  * [3.1. Kết quả PCA]
  * [3.2. Biểu đồ Scree Plot]
  * [3.3. Bảng Loadings]
  * [3.4. PCA Score]
  * [3.5. Plot Score for PC1 and PC2]
* [4. Phân tích Nhân Tố - FA]
  * [4.1. Kết quả Phân tích nhân tố]
  * [4.2. Kiểm tra độ cung cấp thông tin của nhân tố]
  * [4.3. Hệ số Loangdings]
* [5. Đánh giá các phương pháp]
  * [5.1. So sánh các phương pháp]
  * [5.2. Diễn giải kết quả]
  * [5.3. Nhận xét]
* [6. Kết luận]
## Giới thiệu

- Bộ dữ liệu: [Introvert, Extrovert & Ambivert Classification](https://www.kaggle.com/datasets/miadul/introvert-extrovert-and-ambivert-classification) (Bộ dữ liệu đặc điểm tính cách tổng hợp: Phân loại hướng nội, hướng ngoại và ambivert) thu thập từ Kaggle, bộ dữ liệu tổng hợp này được thiết kế để mô phỏng các loại tính cách của con người — Hướng nội, Hướng ngoại và cả người có cả hướng ngoại lẫn hướng nội — dựa trên nhiều đặc điểm hành vi và tâm lý khác nhau.
- Bộ dữ liệu này chứa 20.000 mục nhập và 30 cột, bao gồm 29 đặc điểm số biểu thị các chỉ số tính cách và 1 cột nhãn (personality\_type).
- Mục tiêu của báo cáo là phân tích các yếu tố ảnh hưởng tính cách, đặc biệt tập trung vào các yếu tố liên quan đến cách, thông qua các phương pháp phân tích thành phần chính (PCA), phân tích nhân tố (FA).

## Tiền xử lý dữ liệu
### Đọc và kiểm tra dữ liệu
Bộ dữ liệu này chứa 20.000 mục nhập và 30 cột, bao gồm 29 đặc điểm số biểu thị các chỉ số tính cách và 1 cột nhãn (personality_type).
Trong đó:
- personality\_type: biến mục tiêu gồm 3 kiểu tính cách: Introvert(hướng
  nội), Extrovert(hướng ngoại), or Ambivert (hỗn hợp).
- social\_energy: Xu hướng đón nhận năng lượng từ tương tác xã hội
  (0--10).
- alone\_time\_preference: thể hiện sự thoải mái với sự cô đơn.
- talkativeness: Xu hướng tham gia và các cuộc trò chuyện.
- deep\_reflection: Tần suất suy nghĩ sâu hoặc suy nghĩ nội tâm.
- group\_comfort: Dễ hoà nhập với các nhóm/ hội.
- party\_liking: Sự thích thú đối với các bữa tiệc và các sự kiện.
- listening\_skill: Khả năng lắng nghe
- empathy: khả năng đồng cảm hay thấu hiểu cảm xúc của người khác.
- creativity: sự tư duy sáng tạo.
- organization: Mức độ ưu tiên cho các trật tự, kế hoạch.
- leadership: Sự thoải mái khi làm lãnh đạo.
- risk\_taking: Sự chấp nhận rủi ro.
- public\_speaking\_comfort: Mức độ thoải mái khi nói chuyện trước đám
  đông hoặc công chúng.
- curiosity: Mức độ thích học tập và khám phá những cái mới.
- routine\_preference: Thể hiện thói quen và sự tự phát.
- excitement\_seeking: Mức độ mong muốn những trải nghiệm mới mẻ.
- friendliness: Mức độ thân thiện.
- emotional\_stability: Khả năng kiểm soát và cân bằng khi căng thẳng.
- planning: Xu hướng lập kế hoạch từ trước.
- spontaneity: Hành động tự phát không có kế hoạch từ trước.
- adventurousness: Sẵn sàng thử những hoạt động mới và mạo hiểm.
- reading\_habit: Tần suất đọc sách báo.
- sports\_interest: Mức độ quan tâm tới thể thao hoặc các hoạt động thể
  chất.
- online\_social\_usage: Thời gian dành cho mạng xã hội.
- travel\_desire: Sở thích du lịch và khám phá những địa điểm mới.
- gadget\_usage: Tần suất sử dụng các thiết bị công nghệ và tiện ích.
- work\_style\_collaborative: mức độ làm việc nhóm so với với việc làm
  cá nhân.
- decision\_speed: Thời gian đưa ra các quyết định.
- stress\_handling: Khả năng quản lý căng thẳng cách hiệu quả.

**Nhận xét:**
- Các biến đều có giá trị numeric. Chỉ có biến personality\_type là biến mục tiêu.
- Ta thấy bộ dữ liệu này khảo sát với số lượng người thuộc từng nhóm xấp xỉ nhau:
  - Ambivert: 6573
  - Extrovert: 6857
  - Introvert: 657
Các biến còn lại đều là thang đo từ 1-10.
- Bộ dữ liệu không có giá trị nào bị thiếu.

### Kiểm tra và xử lý giá trị ngoại lai
Vẽ đồ thị boxplot cho bộ dữ liệu mà ta xét PCA
**Nhận xét:** Ta nhận thấy có các giá trị ngoại lai ở một số biến.
- Vì đây là bộ dữ liệu nhiều chiều nên không thể sử dụng IQR để xác định các giá trị ngoại lai mà cần sử dụng khoảng cách Mahalanobis để xác định các giá trị ngoại lai.
- có 821 giá trị ngoại lai chiếm 4,105\% giá trị quan trắc bộ dữ liệu. Vì số lượng ngoại lai không lớn nên ta tiến hành loại bỏ các giá
trị này.
- kiểm tra lại bộ dữ liệu sau khi loại bỏ giá trị ngoại lai còn 19,179 quan trắc

## Phân tích thành phần chính
### kết quả PCA

**Nhận xét:**
- Theo nguyên tắc Kaiser, nên giữ lại 3 thành phần chính (PC1, PC2,
  PC3), vì chỉ các thành phần này có trị riêng lớn hơn 1.
- Ba thành phần chính đầu tiên thoả nguyên tắc Kaiser tỉ lệ phương sai
  đóng góp là 48,596\%.
- Ta thấy từ thành phần chính thứ nhất (PC1) chiếm 41,62\% tỉ lệ phương
  sai, chiếm phần lớn biến động.
- Nhưng từ thành phần chính thứ 2 trở đi thì tỉ lệ đóng góp phương sai
  giảm mạnh chỉ còn dưới 4\%. Ta có thể suy đoán từ thành phần chính thứ
  2 sẽ có các đóng góp vào phương sai của bộ dữ liệu là rất nhỏ. Dựa vào
  tỉ lệ đóng góp phương sai có thể nhận 2 thành phần chính là PC1 và PC2
  bỏ qua nguyên tắc Kaiser.

**Nhận xét:** Thông qua biểu đồ khủy tay
- PC1: Giải thích khoảng 40\% phương sai.
- PC2 từ trở đi: Giảm mạnh xuống dưới mức 4\% phương sai, đồ thị bắt đầu
  thoải ra. Phù hợp với nhận định ở trên là chỉ nên giữ lại 2 thành phần
  chính là PC1 và PC2.
- Điểm elbow có thể xác định là điểm PC2.

### Bảng loadings
- PC1 (Thành phần chính đầu tiên)
  - Biến đóng góp lớn (tuyệt đối = 0.3):
  - social\_energy: -0.2354584797 (âm, tương quan nghịch).
  - alone\_time\_preference: 0.237749517 (dương, ưa thích thời gian một
mình).
  - talkativeness: -0.2372408347 (âm, ít nói chuyện).
  - deep\_reflection: 0.2161623835 (dương, suy ngẫm sâu).
  - group\_comfort: -0.2195160341 (âm, không thoải mái trong nhóm).
  - party\_liking: -0.2493799053 (âm, không thích tiệc tùng).
  - listening\_skill: 0.1468725243 (dương, nhẹ, kỹ năng lắng nghe).

**Nhận xét:** PC1 dường như đại diện cho xu hướng hướng nội (introversion)
so với hướng ngoại (extraversion). Các biến như ưa thích thời gian một
mình, suy ngẫm sâu, và không thoải mái trong nhóm có tải dương, trong
khi năng lượng xã hội, nói chuyện, và thích tiệc tùng có tải âm.

- PC2 (Thành phần chính thứ hai)
  - Biến đóng góp lớn:
    - empathy: 0.59369963 (dương, rất mạnh, đồng cảm).
    - creativity: 0.5966071 (dương, sáng tạo).
    - organization: -0.006812303 (gần 0, không ảnh hưởng).
    - leadership: 0.00393648 (gần 0, không ảnh hưởng).
    - risk\_taking: -0.0163788 (gần 0).
**Nhận xét:** PC2 có thể đại diện cho khả năng cảm xúc và sáng tạo. Biến
empathy và creativity có tải rất cao, trong khi các biến liên quan đến
tổ chức hoặc rủi ro gần như không ảnh hưởng.

**Kết luận:** Dựa trên ma trận tải, chỉ 2 PC đầu tiên có các giá trị tải
đáng kể ( > 0.3 hoặc < -0.3) trên một số biến.
- Điều này phù hợp với phân tích Scree Plot (giữ 2 thành phần đầu).

### PCA score
- PC1 (Thành phần chính đầu tiên)
  - Quan sát nổi bật:
    - Dòng 1: -4.95088554 (rất âm, nổi bật ở hướng ngược).
    - Dòng 2: 0.01836153 (gần 0, trung bình).
    - Dòng 3: 0.43470228 (dương nhẹ).
    - Dòng 5: 3.37129356 (rất dương, nổi bật ở hướng thuận).
**Nhận xét:** PC1 có biên độ lớn (-4.95 đến 3.37), phản ánh sự khác biệt
mạnh giữa các quan sát. Dựa trên ma trận tải trước, PC1 liên quan đến
hướng nội/hướng ngoại, nên các quan sát như dòng 1 (âm) có thể nghiêng
về hướng ngoại, trong khi dòng 5 (dương) nghiêng về hướng nội.
- PC2 (Thành phần chính thứ hai)
  - Quan sát nổi bật:
    - Dòng 1: 0.5999770 (dương nhẹ).
    - Dòng 3: -1.5505420 (âm, nổi bật).
    - Dòng 5: -1.7210118 (âm, nổi bật).
**Nhận xét:** PC2 có biên độ từ -1.72 đến 0.60, liên quan đến cảm xúc/sáng
tạo (theo ma trận tải). Quan sát dòng 3 và 5 có xu hướng thấp về đồng
cảm/sáng tạo, trong khi dòng 1 cao hơn.

### Score plot for PC1 and PC2
**Biến có tải lớn trên PC1 (hướng ngang)**

1. Biến âm (bên trái, PC1 < 0):
- social\_energy, talkativeness, party\_liking, group\_comfort: Các biến
này có tải âm trên PC1, gợi ý PC1 phân biệt hướng ngoại (âm) so với
hướng nội (dương). Những người có giá trị âm trên PC1 có xu hướng năng
động xã hội.

2. Biến dương (bên phải, PC1 >= 0):
- alone\_time\_preference, deep\_reflection: Các biến này có tải dương,
liên quan đến xu hướng hướng nội, ưa thích thời gian một mình và suy
ngẫm sâu.

**Biến có tải lớn trên PC2 (hướng dọc)**

1. Biến dương (trên, PC2 > 0):
- curiosity, empathy, planning, listening\_skill, organization,
routine\_preference: Các biến này có tải dương trên PC2, cho thấy PC2 có
thể liên quan đến khả năng cảm xúc (empathy), tổ chức (planning,
organization), và sự tò mò (curiosity).

2. Biến âm (dưới, PC2 < 0):

- Ít biến nổi bật ở phía âm, nhưng một số như decision\_speed có thể có
tải nhẹ âm.

3. Biến có độ dài mũi tên lớn

- curiosity, empathy, planning: Có mũi tên dài, cho thấy chúng đóng góp
mạnh vào sự phân biệt giữa PC1 và PC2.

- social\_energy, alone\_time\_preference: Cũng có độ dài đáng kể, nhấn
mạnh vai trò của chúng trong PC1.

**Ý nghĩa:* PC1 chủ yếu phân biệt hướng nội (introversion) và hướng ngoại
(extraversion), trong khi PC2 liên quan đến khả năng cảm xúc, tổ chức,
và tò mò. Điều này phù hợp với ma trận tải trước.\\

**Nhận xét:**

Phân biệt rõ ràng: PC1 phân biệt tốt ba nhóm tính cách:

- Extravert (âm) vs Introvert (dương), với Ambivert ở giữa, xác nhận PC1
là trục hướng nội/hướng ngoại.

- PC2 không phân biệt rõ ràng giữa các nhóm, nhưng cho thấy sự đa dạng nội
bộ (ví dụ: Introvert có điểm cao trên PC2 có thể liên quan đến tò mò).

- Độ chồng lấn: Có một số chồng lấn giữa Ambivert và hai nhóm còn lại, đặc
biệt ở vùng PC1 gần 0, phản ánh tính chất trung gian của Ambivert.

- Phân bố đều: Mỗi nhóm có số lượng quan sát đáng kể, với Extravert và
Introvert có biên độ rộng hơn, trong khi Ambivert tập trung hơn.

# Phân tích nhân tố
Trước khi phân tích nhân tố thì bộ dữ liệu xét phải được chuẩn hóa, ta tiến hành chuẩn hóa và phân tích nhân tố.
## Kết quả phân tích nhân tố
**Nhận xét:* với giá trị p\_value = 0.149 > 0.05
chứng tỏ không đủ cơ sở bác bỏ việc phân tích dựa trên 2 nhân tố là
không thể hiện đầy đủ thông tin của bộ dữ liệu. Vì vậy ta nhận việc phân
tích bộ dữ liệu dựa trên 2 nhân tố.

### Kiểm tra độ cung cấp thông tin của nhân tố
**Nhận xét:**
- đây là các biến có hệ số lớn, có nghĩa chúng chia sẻ rất nhiều phương
  sai của nó với các biến khác: social\_energy,alone\_time\_preference,
  talkativeness, deep\_reflection , group\_comfort, party\_liking,
  leadership, risk\_taking, public\_speaking\_comfort,
  excitement\_seeking, adventurousness. reading\_habit.
- nhưng có một số biến gần như bằng 0 như là stress\_handling,
  creativity, emotional\_stability,empathy. gần như chúng không chia sẻ
  bất cứ một thông tin nào. vì có sự chênh lệch như vậy nên ta sẽ thử
  xoay nhân tố theo ``varimax'' xem thử có thay đổi chút gì được không.

**Nhận xét:** Sau khi xoay ta cũng không nhận lại được gì nhiều
thay đổi nên vì vậy ta sẽ phân tích hệ số tải của FA luôn.

### Hệ số tải
### Nhận xét:
- các biến có hệ số lớn hơn 0 như là:
    social\_energy,talkativeness,group\_comfort, party\_liking,
    leadership,risk\_taking,public\_speaking\_comfort,curiosity,
    excitement\_seeking,friendliness ,spontaneity,
    adventurousness,sports\_interest ,online\_social\_usage,
    travel\_desire,gadget\_usage, work\_style\_collaborative,
    decision\_speed
  - Các biến có hệ số \textless{} 0: alone\_time\_preference,
    deep\_reflection, listening\_skill, empathy, organization,
    routine\_preference, routine\_preference, planning, reading\_habit,
    stress\_handling =\textgreater{} đây là những tính cách thể hiện một
    người có tính cách hương ngoại và đối lập với điều đó là một người
    hướng nội Từ đây ta có thể thấy factor 1 chính là đại diện nhân tố
    của một người hương ngoại và để dễ dàng nhận biết và phân biệt với
    một người hướng nội.
    
**Ở Factor 2:**
- Biến có hệ số > 0: group\_comfort, friendliness
- Biến có hệ số < 0: deep\_reflection, planning:
    - Đây là nhóm tính cách vừa có một chút của hướng ngoại là thoải mái
    trong nhóm, thân thiện nhưng cũng có chút của hương nội là suy nghĩ
    nội tâm, lập kế hoạch. Từ đây ta có thế thấy factor 2 chính là nhân
    tố ẩn của một người khi họ vừa có chút tính cách hướng ngoại vừa có
    chút tính cách hướng nội hay còn gọi với một cái tên là Ambiver
    (người trung tính), là sự kết hợp giữa một chút hướng ngoại một chút
    hướng nội: đây là người có sự hòa đồng, thân thiện nhưng lại có cái
    nhìn rất sâu sắc đôi khi và bộ dữ liệu đã thể hiện đây là một người
    vừa có yếu tố xã hội vừa có yếu tố nội tâm. mặc ù là hệ số của cả 4
    biến không quá cao nhưng đâu đó ta có thể nhận dạng được sự pha trộn
    này.

**Kết luận:** Từ bộ dữ liệu ta đã nhận dạng được một cách rõ ràng
của người hướng nội và hướng ngoại, nhưng phải qua phân tích nhân tố FA
mà ta thấy rõ được một tính cách tiềm ẩn của một người trung tính là sự
kết hợp một chút hướng ngoại và một chút hướng nội thông qua 2 yếu tố là
xã hội và nội tâm.


## Đánh giá các phương pháp
### So sánh các phương pháp
Phân tích dữ liệu từ bộ dữ liệu "personality\_synthetic\_dataset\_cav" tập trung vào hai phương pháp chính: Phân tích thành phần chính (Principal Component Analysis - PCA) và Phân tích nhân tố (Factor Analysis - FA). Các bước bổ trợ như chuẩn hóa dữ liệu và kiểm tra boxplot được sử dụng để đảm bảo tính hợp lệ của dữ liệu, nhưng không phải trọng tâm.
- Phân tích thành phân chính - PCA: Được sử dụng để khám phá cấu trúc dữ liệu, giảm chiều dữ liệu và xác định các thành phần chính (PC1, PC2) đại diện cho các đặc điểm tính cách, giúp phân biệt các nhóm tính cách (Introvert, Extrovert, Ambivert). PCA hiệu quả trong việc trực quan hóa sự phân bố và phân biệt các nhóm dựa trên các biến như social\_energy, talkativeness, và party\_liking.
- Phân tích nhân tố (FA): Được áp dụng trên dữ liệu chuẩn hóa (data\_sc) để giảm chiều dữ liệu, xác định các yếu tố tiềm ẩn (latent factors) đại diện cho các đặc điểm tính cách (ví dụ: hướng ngoại, hướng nội), và giảm thiểu tác động của các biến có tương quan cao (như social\_energy và talkativeness).
\textbf{So sánh:}
- PCA hiệu quả trong việc giảm chiều dữ liệu và trực quan hóa sự phân biệt giữa các nhóm tính cách, đặc biệt với PC1 (hướng nội/hướng ngoại), nhưng không cung cấp giải thích rõ ràng về các yếu tố tiềm ẩn.
- FA tập trung vào việc xác định các yếu tố tiềm ẩn (như hướng ngoại, hướng nội) và giải thích mối quan hệ giữa các biến, nhưng việc giải thích nhân tố có thể phức tạp và phụ thuộc vào số lượng nhân tố được chọn.

### Diễn giải kết quả

Phân tích thành phần chính (PCA):
- PC1 phân biệt rõ ràng giữa Extrovert (âm) và Introvert (dương), với Ambivert nằm ở giữa, xác nhận PC1 đại diện cho trục hướng nội/hướng ngoại.
- PC2 cho thấy sự đa dạng trong nhóm Introvert (ví dụ, liên quan đến tò mò hoặc suy ngẫm), nhưng không phân biệt rõ ràng giữa các nhóm.
- Biểu đồ điểm (score plot) cho thấy sự chồng lấn giữa Ambivert và các nhóm khác ở vùng PC1 gần 0, phản ánh tính chất trung gian của Ambivert.
Phân tích nhân tố (FA): FA với hai nhân tố cho thấy:
- Nhân tố 1 (Hướng ngoại): Bao gồm các biến như social\_energy (0.808), talkativeness (0.816), group\_comfort (0.742), party\_liking (0.862), leadership (0.743), risk\_taking (0.739), public\_speak\\-ing\_comfort (0.817), và excitement\_seeking (0.813), phản ánh các đặc điểm liên quan đến sự hướng ngoại, năng động xã hội và chấp nhận rủi ro.

- Nhân tố 2 (Hướng nội): Bao gồm các biến như alone\_time\_preference (-0.816), deep\_reflection (-0.732), và routine\_preference (-0.639), liên quan đến sự hướng nội, suy ngẫm sâu sắc và ưu tiên thói quen.

- Các biến như creativity, emotional\_stability, và stress\_handling có độ chia sẻ phương sai thấp (gần 0), cho thấy chúng không đóng góp đáng kể vào các nhân tố này.

### Nhận xét
- PCA hiệu quả trong việc trực quan hóa sự khác biệt giữa các nhóm tính cách, đặc biệt với PC1 phân biệt rõ ràng giữa Extrovert và Introvert, nhưng PC2 không cung cấp sự phân biệt rõ ràng.
- FA cung cấp cái nhìn sâu sắc về các yếu tố tiềm ẩn (hướng ngoại và hướng nội), giúp xác định các biến quan trọng và giảm chiều dữ liệu, nhưng việc giải thích nhân tố có thể phức tạp khi một số biến (như creativity, emotional\_stability) có đóng góp thấp.

- Các biến như creativity, emotional\_stability, và stress\_handling không đóng góp đáng kể vào phân loại tính cách, ngụ ý chúng có thể không phải là yếu tố chính trong bộ dữ liệu này.

- Kích thước mẫu lớn (19,179 quan trắc) đảm bảo độ tin cậy của phân tích, nhưng sự chồng lấn của Ambivert với các nhóm khác trên PC1 gây khó khăn trong việc phân loại rạch ròi.

## Kết luận

- Bộ dữ liệu "personality\_synthetic\_dataset\_cav" bao gồm 20,000 quan trắc (19,179 sau khi loại bỏ ngoại lai) với 30 biến định lượng, được phân tích chủ yếu bằng PCA và FA.

- PCA cho thấy PC1 phân biệt rõ ràng giữa Extrovert và Introvert, với Ambivert ở giữa, trong khi PC2 phản ánh sự đa dạng trong nhóm Introvert.

- FA xác định hai yếu tố tiềm ẩn: hướng ngoại (liên quan đến social\_energy, talkativeness, party\_liking, v.v.) và hướng nội (liên quan đến alone\_time\_preference, deep\_reflection). Các biến như creativity, emotional\_stability, và stress\_handling không đóng góp đáng kể.

### Ưu điểm phương pháp
- Xử lý dữ liệu sạch: Loại bỏ 821 giá trị ngoại lai và chuẩn hóa dữ liệu đảm bảo chất lượng phân tích, với kích thước mẫu lớn (19,179) tăng độ tin cậy.

- Giảm chiều dữ liệu: PCA và FA giảm chiều dữ liệu hiệu quả, với PCA trực quan hóa sự phân biệt và FA xác định các yếu tố tiềm ẩn.

### Hạn chế

- Hạn chế của một số biến: Các biến như creativity, emotional\_stability, và stress\_handling có đóng góp thấp, làm giảm giá trị của chúng trong phân loại tính cách.

- Chồng lấn của Ambivert: Sự chồng lấn của Ambivert với các nhóm khác trên PC1 gây khó khăn trong việc phân loại rạch ròi.

- Phức tạp trong giải thích FA: Việc xác định và giải thích nhân tố có thể phức tạp khi một số biến có đóng góp yếu.

- Hạn chế của PC2: PC2 không phân biệt rõ ràng giữa các nhóm, làm giảm giá trị giải thích của nó.

\newpage
