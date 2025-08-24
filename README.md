\section{Các yếu tố ảnh hưởng đến phân loại người hướng ngoại, hướng nội}

\subsection{Giới thiệu}

Bộ dữ liệu:\href{https://www.kaggle.com/datasets/miadul/introvert-extrovert-and-ambivert-classification}{personality\_synthetic\_dataset.csv} (Bộ dữ liệu đặc điểm tính cách tổng hợp: Phân loại hướng nội, hướng ngoại và ambivert) thu thập từ Kaggle, bộ dữ liệu tổng hợp này được thiết kế để mô phỏng các loại tính cách của con người — Hướng nội, Hướng ngoại và cả người có cả hướng ngoại lẫn hướng nội — dựa trên nhiều đặc điểm hành vi và tâm lý khác nhau. \\
Bộ dữ liệu này chứa 20.000 mục nhập và 30 cột, bao gồm 29 đặc điểm số biểu thị các chỉ số tính cách và 1 cột nhãn (personality\_type).\\
Mục tiêu của báo cáo là phân tích các yếu tố ảnh hưởng tính cách, đặc biệt tập trung vào các yếu tố liên quan đến cách, thông qua các phương pháp phân tích thành phần chính (PCA), phân tích nhân tố (FA).

\subsection{Tiền xử lý dữ liệu}
\subsubsection{Đọc và kiểm tra dữ liệu}

Bộ dữ liệu này chứa 20.000 mục nhập và 30 cột, bao gồm 29 đặc điểm số biểu thị các chỉ số tính cách và 1 cột nhãn (personality\_type).\\
Trong đó \:
\begin{itemize}
\item
  personality\_type: biến mục tiêu gồm 3 kiểu tính cách: Introvert(hướng
  nội), Extrovert(hướng ngoại), or Ambivert (hỗn hợp).
\item
  social\_energy: Xu hướng đón nhận năng lượng từ tương tác xã hội
  (0--10).
\item
  alone\_time\_preference: thể hiện sự thoải mái với sự cô đơn.
\item
  talkativeness: Xu hướng tham gia và các cuộc trò chuyện.
\item
  deep\_reflection: Tần suất suy nghĩ sâu hoặc suy nghĩ nội tâm.
\item
  group\_comfort: Dễ hoà nhập với các nhóm/ hội.
\item
  party\_liking: Sự thích thú đối với các bữa tiệc và các sự kiện.
\item
  listening\_skill: Khả năng lắng nghe
\item
  empathy: khả năng đồng cảm hay thấu hiểu cảm xúc của người khác.
\item
  creativity: sự tư duy sáng tạo.
\item
  organization: Mức độ ưu tiên cho các trật tự, kế hoạch.
\item
  leadership: Sự thoải mái khi làm lãnh đạo.
\item
  risk\_taking: Sự chấp nhận rủi ro.
\item
  public\_speaking\_comfort: Mức độ thoải mái khi nói chuyện trước đám
  đông hoặc công chúng.
\item
  curiosity: Mức độ thích học tập và khám phá những cái mới.
\item
  routine\_preference: Thể hiện thói quen và sự tự phát.
\item
  excitement\_seeking: Mức độ mong muốn những trải nghiệm mới mẻ.
\item
  friendliness: Mức độ thân thiện.
\item
  emotional\_stability: Khả năng kiểm soát và cân bằng khi căng thẳng.
\item
  planning: Xu hướng lập kế hoạch từ trước.
\item
  spontaneity: Hành động tự phát không có kế hoạch từ trước.
\item
  adventurousness: Sẵn sàng thử những hoạt động mới và mạo hiểm.
\item
  reading\_habit: Tần suất đọc sách báo.
\item
  sports\_interest: Mức độ quan tâm tới thể thao hoặc các hoạt động thể
  chất.
\item
  online\_social\_usage: Thời gian dành cho mạng xã hội.
\item
  travel\_desire: Sở thích du lịch và khám phá những địa điểm mới.
\item
  gadget\_usage: Tần suất sử dụng các thiết bị công nghệ và tiện ích.
\item
  work\_style\_collaborative: mức độ làm việc nhóm so với với việc làm
  cá nhân.
\item
  decision\_speed: Thời gian đưa ra các quyết định.
\item
  stress\_handling: Khả năng quản lý căng thẳng cách hiệu quả.
\end{itemize}


Nhận xét: Các biến đều có giá trị numeric. Chỉ có biến
``personality\_type'' là biến mục tiêu.

Nhận xét: Ta thấy bộ dữ liệu này khảo sát với số lượng người thuộc từng
nhóm \~ nhau:

\begin{itemize}
\item
  Ambivert: 6573
\item
  Extrovert: 6857
\item
  Introvert: 657
\end{itemize}
Các biến còn lại đều là thang đo từ 1-10.\\
\textbf{Nhận xét:} Bộ dữ liệu không có giá trị nào bị thiếu.

\subsubsection{Kiểm tra và xử lý giá trị ngoại lai}
Vẽ đồ thị boxplot cho bộ dữ liệu mà ta xét PCA\\
\pandocbounded{\includegraphics[width=0.8\linewidth]{BaoCao/data3/anh/anh1.png}}\\
\textbf{Nhận xét:} Ta nhận thấy có các giá trị ngoại lai ở một số biến.\\
- Vì đây là bộ dữ liệu nhiều chiều nên không thể sử dụng IQR để xác định các giá trị ngoại lai mà cần sử dụng khoảng cách Mahalanobis để xác định các giá trị ngoại lai.\\
\textbf{Nhận xét:} có 821 giá trị ngoại lai chiếm 4,105\% giá trị quan trắc bộ dữ
liệu. Vì số lượng ngoại lai không lớn nên ta tiến hành loại bỏ các giá
trị này.\\

Vẽ lại boxplot sau khi loại bỏ các giá trị ngoại lai\\
\pandocbounded{\includegraphics[width=0.8\linewidth]{BaoCao/data3/anh/anh2.png}}\\

Kiểm tra lại bộ dữ liệu sau khi loại bỏ giá trị ngoại lai còn 19,179 quan trắc

\subsection{Phân tích thành phần chính}
\subsubsection{kết quả PCA}
\begin{verbatim}
## Importance of components:
##                           PC1     PC2     PC3     PC4     PC5     PC6     PC7
## Standard deviation     3.4743 1.00879 1.00226 0.99460 0.96404 0.96298 0.88075
## Proportion of Variance 0.4162 0.03509 0.03464 0.03411 0.03205 0.03198 0.02675
## Cumulative Proportion  0.4162 0.45132 0.48596 0.52007 0.55212 0.58410 0.61085
##                            PC8     PC9   PC10    PC11    PC12    PC13    PC14
## Standard deviation     0.87784 0.87198 0.8650 0.85581 0.77528 0.77209 0.77019
## Proportion of Variance 0.02657 0.02622 0.0258 0.02526 0.02073 0.02056 0.02046
## Cumulative Proportion  0.63742 0.66364 0.6894 0.71470 0.73542 0.75598 0.77643
##                           PC15   PC16    PC17    PC18    PC19    PC20    PC21
## Standard deviation     0.76691 0.7635 0.75748 0.73347 0.67616 0.67019 0.66767
## Proportion of Variance 0.02028 0.0201 0.01979 0.01855 0.01577 0.01549 0.01537
## Cumulative Proportion  0.79671 0.8168 0.83660 0.85515 0.87092 0.88641 0.90178
##                           PC22   PC23    PC24    PC25    PC26    PC27    PC28
## Standard deviation     0.66345 0.6596 0.61951 0.58181 0.57866 0.57463 0.57346
## Proportion of Variance 0.01518 0.0150 0.01323 0.01167 0.01155 0.01139 0.01134
## Cumulative Proportion  0.91696 0.9320 0.94519 0.95687 0.96841 0.97980 0.99114
##                           PC29
## Standard deviation     0.50697
## Proportion of Variance 0.00886
## Cumulative Proportion  1.00000
\end{verbatim}

\textbf{Nhận xét:}
\begin{itemize}
\item
  Theo nguyên tắc Kaiser, nên giữ lại 3 thành phần chính (PC1, PC2,
  PC3), vì chỉ các thành phần này có trị riêng lớn hơn 1.
\item
  Ba thành phần chính đầu tiên thoả nguyên tắc Kaiser tỉ lệ phương sai
  đóng góp là 48,596\%
\item
  Ta thấy từ thành phần chính thứ nhất (PC1) chiếm 41,62\% tỉ lệ phương
  sai, chiếm phần lớn biến động
\item
  Nhưng từ thành phần chính thứ 2 trở đi thì tỉ lệ đóng góp phương sai
  giảm mạnh chỉ còn dưới 4\%. Ta có thể suy đoán từ thành phần chính thứ
  2 sẽ có các đóng góp vào phương sai của bộ dữ liệu là rất nhỏ. Dựa vào
  tỉ lệ đóng góp phương sai có thể nhận 2 thành phần chính là PC1 và PC2
  bỏ qua nguyên tắc Kaiser
\end{itemize}
\subsubsection{Biểu đồ Scree plot}
\begin{center}
\pandocbounded{\includegraphics[width=0.8\linewidth]{BaoCao/data3/anh/anh3.png}}\\
\end{center}
\textbf{Nhận xét:}

\begin{itemize}
\item
  PC1: Giải thích khoảng 40\% phương sai.
\item
  PC2 từ trở đi: Giảm mạnh xuống dưới mức 4\% phương sai, đồ thị bắt đầu
  thoải ra. Phù hợp với nhận định ở trên là chỉ nên giữ lại 2 thành phần
  chính là PC1 và PC2.
\item
  Điểm elbow có thể xác định là điểm PC2.
\end{itemize}
\subsubsection{Bảng loadings}
\begin{itemize}
\tightlist
\item
  PC1 (Thành phần chính đầu tiên)
\end{itemize}

Biến đóng góp lớn (tuyệt đối \textgreater{} 0.3):

- social\_energy: -0.2354584797 (âm, liên quan ngược).

- alone\_time\_preference: 0.237749517 (dương, ưa thích thời gian một
mình).

- talkativeness: -0.2372408347 (âm, ít nói chuyện).

- deep\_reflection: 0.2161623835 (dương, suy ngẫm sâu).

- group\_comfort: -0.2195160341 (âm, không thoải mái trong nhóm).

- party\_liking: -0.2493799053 (âm, không thích tiệc tùng).

- listening\_skill: 0.1468725243 (dương, nhẹ, kỹ năng lắng nghe).

\textbf{Nhận xét:} PC1 dường như đại diện cho xu hướng hướng nội (introversion)
so với hướng ngoại (extraversion). Các biến như ưa thích thời gian một
mình, suy ngẫm sâu, và không thoải mái trong nhóm có tải dương, trong
khi năng lượng xã hội, nói chuyện, và thích tiệc tùng có tải âm.

\begin{itemize}
\tightlist
\item
  PC2 (Thành phần chính thứ hai)
\end{itemize}

Biến đóng góp lớn:

- empathy: 0.59369963 (dương, rất mạnh, đồng cảm).

- creativity: 0.5966071 (dương, sáng tạo).

- organization: -0.006812303 (gần 0, không ảnh hưởng).

- leadership: 0.00393648 (gần 0, không ảnh hưởng).

- risk\_taking: -0.0163788 (gần 0).

\textbf{Nhận xét:} PC2 có thể đại diện cho khả năng cảm xúc và sáng tạo. Biến
empathy và creativity có tải rất cao, trong khi các biến liên quan đến
tổ chức hoặc rủi ro gần như không ảnh hưởng.

\textbf{Kết luận:} Dựa trên ma trận tải, chỉ 2 PC đầu tiên có các giá trị tải
đáng kể (\textgreater{} 0.3 hoặc \textless{} -0.3) trên một số biến.
Điều này phù hợp với phân tích Scree Plot (giữ 2 thành phần đầu).

\subsubsection{PCA score}
\begin{itemize}
\tightlist
\item
  PC1 (Thành phần chính đầu tiên)
\end{itemize}

Quan sát nổi bật:

- Dòng 1: -4.95088554 (rất âm, nổi bật ở hướng ngược).

- Dòng 2: 0.01836153 (gần 0, trung bình).

- Dòng 3: 0.43470228 (dương nhẹ).

- Dòng 5: 3.37129356 (rất dương, nổi bật ở hướng thuận).

\textbf{Nhận xét:} PC1 có biên độ lớn (-4.95 đến 3.37), phản ánh sự khác biệt
mạnh giữa các quan sát. Dựa trên ma trận tải trước, PC1 liên quan đến
hướng nội/hướng ngoại, nên các quan sát như dòng 1 (âm) có thể nghiêng
về hướng ngoại, trong khi dòng 5 (dương) nghiêng về hướng nội.

\begin{itemize}
\tightlist
\item
  PC2 (Thành phần chính thứ hai)
\end{itemize}

Quan sát nổi bật:

- Dòng 1: 0.5999770 (dương nhẹ).

- Dòng 3: -1.5505420 (âm, nổi bật).

- Dòng 5: -1.7210118 (âm, nổi bật).

\textbf{Nhận xét:} PC2 có biên độ từ -1.72 đến 0.60, liên quan đến cảm xúc/sáng
tạo (theo ma trận tải). Quan sát dòng 3 và 5 có xu hướng thấp về đồng
cảm/sáng tạo, trong khi dòng 1 cao hơn.

\subsubsection{Score plot for PC1 and PC2}
\pandocbounded{\includegraphics[width=0.8\linewidth]{BaoCao/data3/anh/anh4.png}}\\

\textbf{Biến có tải lớn trên PC1 (hướng ngang)}

1. Biến âm (bên trái, PC1 \textless{} 0): \\
- social\_energy, talkativeness, party\_liking, group\_comfort: Các biến
này có tải âm trên PC1, gợi ý PC1 phân biệt hướng ngoại (âm) so với
hướng nội (dương). Những người có giá trị âm trên PC1 có xu hướng năng
động xã hội.

2. Biến dương (bên phải, PC1 \textgreater{} 0):

- alone\_time\_preference, deep\_reflection: Các biến này có tải dương,
liên quan đến xu hướng hướng nội, ưa thích thời gian một mình và suy
ngẫm sâu.

\textbf{Biến có tải lớn trên PC2 (hướng dọc)}

1. Biến dương (trên, PC2 \textgreater{} 0):

- curiosity, empathy, planning, listening\_skill, organization,
routine\_preference: Các biến này có tải dương trên PC2, cho thấy PC2 có
thể liên quan đến khả năng cảm xúc (empathy), tổ chức (planning,
organization), và sự tò mò (curiosity).

2. Biến âm (dưới, PC2 \textless{} 0):

- Ít biến nổi bật ở phía âm, nhưng một số như decision\_speed có thể có
tải nhẹ âm.

3. Biến có độ dài mũi tên lớn

- curiosity, empathy, planning: Có mũi tên dài, cho thấy chúng đóng góp
mạnh vào sự phân biệt giữa PC1 và PC2.

- social\_energy, alone\_time\_preference: Cũng có độ dài đáng kể, nhấn
mạnh vai trò của chúng trong PC1.

\textbf{Ý nghĩa:} PC1 chủ yếu phân biệt hướng nội (introversion) và hướng ngoại
(extraversion), trong khi PC2 liên quan đến khả năng cảm xúc, tổ chức,
và tò mò. Điều này phù hợp với ma trận tải trước.\\

\pandocbounded{\includegraphics[width=0.8\linewidth]{BaoCao/data3/anh/anh5.png}}\\
\textbf{Nhận xét:}

Phân biệt rõ ràng: PC1 phân biệt tốt ba nhóm tính cách:

- Extravert (âm) vs Introvert (dương), với Ambivert ở giữa, xác nhận PC1
là trục hướng nội/hướng ngoại.

- PC2 không phân biệt rõ ràng giữa các nhóm, nhưng cho thấy sự đa dạng nội
bộ (ví dụ: Introvert có điểm cao trên PC2 có thể liên quan đến tò mò).

- Độ chồng lấn: Có một số chồng lấn giữa Ambivert và hai nhóm còn lại, đặc
biệt ở vùng PC1 gần 0, phản ánh tính chất trung gian của Ambivert.

- Phân bố đều: Mỗi nhóm có số lượng quan sát đáng kể, với Extravert và
Introvert có biên độ rộng hơn, trong khi Ambivert tập trung hơn.

\subsection{Phân tích nhân tố}
Trước khi phân tích nhân tố thì bộ dữ liệu xét phải được chuẩn hóa, ta tiến hành chuẩn hóa và phân tích nhân tố.\\
\pandocbounded{\includegraphics[width=0.8\linewidth]{BaoCao/data3/anh/anh6.png}}\\
\subsubsection{Kết quả phân tích nhân tố}
\begin{verbatim}
## 
## Call:
## factanal(x = data_sc, factors = 2)
## 
## Uniquenesses:
##            social_energy    alone_time_preference            talkativeness 
##                    0.342                    0.328                    0.331 
##          deep_reflection            group_comfort             party_liking 
##                    0.451                    0.436                    0.249 
##          listening_skill                  empathy               creativity 
##                    0.760                    0.931                    1.000 
##             organization               leadership              risk_taking 
##                    0.763                    0.442                    0.453 
##  public_speaking_comfort                curiosity       routine_preference 
##                    0.331                    0.933                    0.591 
##       excitement_seeking             friendliness      emotional_stability 
##                    0.336                    0.750                    0.998 
##                 planning              spontaneity          adventurousness 
##                    0.746                    0.592                    0.446 
##            reading_habit          sports_interest      online_social_usage 
##                    0.442                    0.581                    0.593 
##            travel_desire             gadget_usage work_style_collaborative 
##                    0.593                    0.760                    0.593 
##           decision_speed          stress_handling 
##                    0.584                    1.000 
## 
## Loadings:
##                          Factor1 Factor2
## social_energy             0.808         
## alone_time_preference    -0.816         
## talkativeness             0.816         
## deep_reflection          -0.732  -0.115 
## group_comfort             0.742   0.116 
## party_liking              0.862         
## listening_skill          -0.482         
## empathy                  -0.260         
## creativity                              
## organization             -0.483         
## leadership                0.743         
## risk_taking               0.739         
## public_speaking_comfort   0.817         
## curiosity                 0.259         
## routine_preference       -0.639         
## excitement_seeking        0.813         
## friendliness              0.480   0.138 
## emotional_stability                     
## planning                 -0.467  -0.189 
## spontaneity               0.637         
## adventurousness           0.742         
## reading_habit            -0.740         
## sports_interest           0.645         
## online_social_usage       0.637         
## travel_desire             0.637         
## gadget_usage              0.486         
## work_style_collaborative  0.638         
## decision_speed            0.644         
## stress_handling                         
## 
##                Factor1 Factor2
## SS loadings     11.489   0.155
## Proportion Var   0.396   0.005
## Cumulative Var   0.396   0.402
## 
## Test of the hypothesis that 2 factors are sufficient.
## The chi square statistic is 376.5 on 349 degrees of freedom.
## The p-value is 0.149
\end{verbatim}

\textbf{Nhận xét:} với giá trị p\_value = 0.149 \textgreater{} 0.05
chứng tỏ không đủ cơ sở bác bỏ việc phân tích dựa trên 2 nhân tố là
không thể hiện đầy đủ thông tin của bộ dữ liệu. Vì vậy ta nhận việc phân
tích bộ dữ liệu dựa trên 2 nhân tố.

\subsubsection{Kiểm tra độ cung cấp thông tin của nhân tố}
\begin{verbatim}
##            social_energy    alone_time_preference            talkativeness 
##                    0.658                    0.672                    0.669 
##          deep_reflection            group_comfort             party_liking 
##                    0.549                    0.564                    0.751 
##          listening_skill                  empathy               creativity 
##                    0.240                    0.069                    0.000 
##             organization               leadership              risk_taking 
##                    0.237                    0.558                    0.547 
##  public_speaking_comfort                curiosity       routine_preference 
##                    0.669                    0.067                    0.409 
##       excitement_seeking             friendliness      emotional_stability 
##                    0.664                    0.250                    0.002 
##                 planning              spontaneity          adventurousness 
##                    0.254                    0.408                    0.554 
##            reading_habit          sports_interest      online_social_usage 
##                    0.558                    0.419                    0.407 
##            travel_desire             gadget_usage work_style_collaborative 
##                    0.407                    0.240                    0.407 
##           decision_speed          stress_handling 
##                    0.416                    0.000
\end{verbatim}

\textbf{Nhận xét:}

\begin{itemize}
\item
  đây là các biến có hệ số lớn, có nghĩa chúng chia sẻ rất nhiều phương
  sai của nó với các biến khác: social\_energy,alone\_time\_preference,
  talkativeness, deep\_reflection , group\_comfort, party\_liking,
  leadership, risk\_taking, public\_speaking\_comfort,
  excitement\_seeking, adventurousness. reading\_habit.
\item
  nhưng có một số biến gần như bằng 0 như là stress\_handling,
  creativity, emotional\_stability,empathy. gần như chúng không chia sẻ
  bất cứ một thông tin nào. vì có sự chênh lệch như vậy nên ta sẽ thử
  xoay nhân tố theo ``varimax'' xem thử có thay đổi chút gì được không.
\end{itemize}

\textbf{Nhận xét:} Sau khi xoay ta cũng không nhận lại được gì nhiều
thay đổi nên vì vậy ta sẽ phân tích hệ số tải của FA luôn.

\subsubsection{Hệ số tải}
\begin{verbatim}
## 
## Loadings:
##                          Factor1 Factor2
## social_energy             0.808         
## alone_time_preference    -0.816         
## talkativeness             0.816         
## deep_reflection          -0.732  -0.115 
## group_comfort             0.742   0.116 
## party_liking              0.862         
## listening_skill          -0.482         
## empathy                  -0.260         
## creativity                              
## organization             -0.483         
## leadership                0.743         
## risk_taking               0.739         
## public_speaking_comfort   0.817         
## curiosity                 0.259         
## routine_preference       -0.639         
## excitement_seeking        0.813         
## friendliness              0.480   0.138 
## emotional_stability                     
## planning                 -0.467  -0.189 
## spontaneity               0.637         
## adventurousness           0.742         
## reading_habit            -0.740         
## sports_interest           0.645         
## online_social_usage       0.637         
## travel_desire             0.637         
## gadget_usage              0.486         
## work_style_collaborative  0.638         
## decision_speed            0.644         
## stress_handling                         
## 
##                Factor1 Factor2
## SS loadings     11.489   0.155
## Proportion Var   0.396   0.005
## Cumulative Var   0.396   0.402
\end{verbatim}

\textbf{Nhận xét:}

\begin{itemize}
\tightlist
\item
  Ở factor 1:

  \begin{itemize}
  \tightlist
  \item
    các biến có hệ số lớn hơn 0 như là:
    social\_energy,talkativeness,group\_comfort, party\_liking,
    leadership,risk\_taking,public\_speaking\_comfort,curiosity,
    excitement\_seeking,friendliness ,spontaneity,
    adventurousness,sports\_interest ,online\_social\_usage,
    travel\_desire,gadget\_usage, work\_style\_collaborative,
    decision\_speed
  \item
    Các biến có hệ số \textless{} 0: alone\_time\_preference,
    deep\_reflection, listening\_skill, empathy, organization,
    routine\_preference, routine\_preference, planning, reading\_habit,
    stress\_handling =\textgreater{} đây là những tính cách thể hiện một
    người có tính cách hương ngoại và đối lập với điều đó là một người
    hướng nội Từ đây ta có thể thấy factor 1 chính là đại diện nhân tố
    của một người hương ngoại và để dễ dàng nhận biết và phân biệt với
    một người hướng nội
  \end{itemize}
\item
  Ở Factor 2:

  \begin{itemize}
  \tightlist
  \item
    Biến có hệ số \textgreater0: group\_comfort, friendliness
  \item
    Biến có hệ số \textless0: deep\_reflection, planning =\textgreater{}
    Đây là nhóm tính cách vừa có một chút của hướng ngoại là thoải mái
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
  \end{itemize}
\end{itemize}

\textbf{Kết luận:} Từ bộ dữ liệu ta đã nhận dạng được một cách rõ ràng
của người hướng nội và hướng ngoại, nhưng phải qua phân tích nhân tố FA
mà ta thấy rõ được một tính cách tiềm ẩn của một người trung tính là sự
kết hợp một chút hướng ngoại và một chút hướng nội thông qua 2 yếu tố là
xã hội và nội tâm.


\subsection{Đánh giá các phương pháp}
\subsubsection{So sánh các phương pháp}
Phân tích dữ liệu từ bộ dữ liệu "personality\_synthetic\_dataset\_cav" tập trung vào hai phương pháp chính: Phân tích thành phần chính (Principal Component Analysis - PCA) và Phân tích nhân tố (Factor Analysis - FA). Các bước bổ trợ như chuẩn hóa dữ liệu và kiểm tra boxplot được sử dụng để đảm bảo tính hợp lệ của dữ liệu, nhưng không phải trọng tâm.\\
- Phân tích thành phân chính - PCA: Được sử dụng để khám phá cấu trúc dữ liệu, giảm chiều dữ liệu và xác định các thành phần chính (PC1, PC2) đại diện cho các đặc điểm tính cách, giúp phân biệt các nhóm tính cách (Introvert, Extrovert, Ambivert). PCA hiệu quả trong việc trực quan hóa sự phân bố và phân biệt các nhóm dựa trên các biến như social\_energy, talkativeness, và party\_liking.\\
- Phân tích nhân tố (FA): Được áp dụng trên dữ liệu chuẩn hóa (data\_sc) để giảm chiều dữ liệu, xác định các yếu tố tiềm ẩn (latent factors) đại diện cho các đặc điểm tính cách (ví dụ: hướng ngoại, hướng nội), và giảm thiểu tác động của các biến có tương quan cao (như social\_energy và talkativeness).\\
\textbf{So sánh:}\\
- PCA hiệu quả trong việc giảm chiều dữ liệu và trực quan hóa sự phân biệt giữa các nhóm tính cách, đặc biệt với PC1 (hướng nội/hướng ngoại), nhưng không cung cấp giải thích rõ ràng về các yếu tố tiềm ẩn.\\
- FA tập trung vào việc xác định các yếu tố tiềm ẩn (như hướng ngoại, hướng nội) và giải thích mối quan hệ giữa các biến, nhưng việc giải thích nhân tố có thể phức tạp và phụ thuộc vào số lượng nhân tố được chọn.

\subsubsection{Diễn giải kết quả}

Phân tích thành phần chính (PCA):
- PC1 phân biệt rõ ràng giữa Extrovert (âm) và Introvert (dương), với Ambivert nằm ở giữa, xác nhận PC1 đại diện cho trục hướng nội/hướng ngoại.
- PC2 cho thấy sự đa dạng trong nhóm Introvert (ví dụ, liên quan đến tò mò hoặc suy ngẫm), nhưng không phân biệt rõ ràng giữa các nhóm.
- Biểu đồ điểm (score plot) cho thấy sự chồng lấn giữa Ambivert và các nhóm khác ở vùng PC1 gần 0, phản ánh tính chất trung gian của Ambivert.\\
Phân tích nhân tố (FA): FA với hai nhân tố cho thấy:\\
- Nhân tố 1 (Hướng ngoại): Bao gồm các biến như social\_energy (0.808), talkativeness (0.816), group\_comfort (0.742), party\_liking (0.862), leadership (0.743), risk\_taking (0.739), public\_speak\\-ing\_comfort (0.817), và excitement\_seeking (0.813), phản ánh các đặc điểm liên quan đến sự hướng ngoại, năng động xã hội và chấp nhận rủi ro.

- Nhân tố 2 (Hướng nội): Bao gồm các biến như alone\_time\_preference (-0.816), deep\_reflection (-0.732), và routine\_preference (-0.639), liên quan đến sự hướng nội, suy ngẫm sâu sắc và ưu tiên thói quen.

- Các biến như creativity, emotional\_stability, và stress\_handling có độ chia sẻ phương sai thấp (gần 0), cho thấy chúng không đóng góp đáng kể vào các nhân tố này.

\subsubsection{Nhận xét}
- PCA hiệu quả trong việc trực quan hóa sự khác biệt giữa các nhóm tính cách, đặc biệt với PC1 phân biệt rõ ràng giữa Extrovert và Introvert, nhưng PC2 không cung cấp sự phân biệt rõ ràng.\\
- FA cung cấp cái nhìn sâu sắc về các yếu tố tiềm ẩn (hướng ngoại và hướng nội), giúp xác định các biến quan trọng và giảm chiều dữ liệu, nhưng việc giải thích nhân tố có thể phức tạp khi một số biến (như creativity, emotional\_stability) có đóng góp thấp.

- Các biến như creativity, emotional\_stability, và stress\_handling không đóng góp đáng kể vào phân loại tính cách, ngụ ý chúng có thể không phải là yếu tố chính trong bộ dữ liệu này.

- Kích thước mẫu lớn (19,179 quan trắc) đảm bảo độ tin cậy của phân tích, nhưng sự chồng lấn của Ambivert với các nhóm khác trên PC1 gây khó khăn trong việc phân loại rạch ròi.

\subsection{Kết luận}

- Bộ dữ liệu "personality\_synthetic\_dataset\_cav" bao gồm 20,000 quan trắc (19,179 sau khi loại bỏ ngoại lai) với 30 biến định lượng, được phân tích chủ yếu bằng PCA và FA.

- PCA cho thấy PC1 phân biệt rõ ràng giữa Extrovert và Introvert, với Ambivert ở giữa, trong khi PC2 phản ánh sự đa dạng trong nhóm Introvert.

- FA xác định hai yếu tố tiềm ẩn: hướng ngoại (liên quan đến social\_energy, talkativeness, party\_liking, v.v.) và hướng nội (liên quan đến alone\_time\_preference, deep\_reflection). Các biến như creativity, emotional\_stability, và stress\_handling không đóng góp đáng kể.

\subsubsection{Ưu điểm phương pháp}
- Xử lý dữ liệu sạch: Loại bỏ 821 giá trị ngoại lai và chuẩn hóa dữ liệu đảm bảo chất lượng phân tích, với kích thước mẫu lớn (19,179) tăng độ tin cậy.

- Giảm chiều dữ liệu: PCA và FA giảm chiều dữ liệu hiệu quả, với PCA trực quan hóa sự phân biệt và FA xác định các yếu tố tiềm ẩn.

\subsubsection{Hạn chế}

- Hạn chế của một số biến: Các biến như creativity, emotional\_stability, và stress\_handling có đóng góp thấp, làm giảm giá trị của chúng trong phân loại tính cách.

- Chồng lấn của Ambivert: Sự chồng lấn của Ambivert với các nhóm khác trên PC1 gây khó khăn trong việc phân loại rạch ròi.

- Phức tạp trong giải thích FA: Việc xác định và giải thích nhân tố có thể phức tạp khi một số biến có đóng góp yếu.

- Hạn chế của PC2: PC2 không phân biệt rõ ràng giữa các nhóm, làm giảm giá trị giải thích của nó.

\newpage
