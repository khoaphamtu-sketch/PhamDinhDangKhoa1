import React, { useState } from 'react';
import { CheckCircle, XCircle, Trophy, RefreshCcw, ArrowRight, Timer, HelpCircle, Play, Star } from 'lucide-react';

const App = () => {
  const [gameState, setGameState] = useState('start'); // start, playing, result
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [score, setScore] = useState(0);
  const [showFeedback, setShowFeedback] = useState(false); 
  const [selectedAnswer, setSelectedAnswer] = useState(null);
  const [isCorrect, setIsCorrect] = useState(false);

  // Bộ 60 câu hỏi F&B
  const questions = [
    { question: "Thuật ngữ '86' trong nhà hàng có nghĩa là gì?", options: ["Món ăn bán chạy nhất", "Hết món hoặc ngừng phục vụ món đó", "Giảm giá 86%", "Mã số của quản lý nhà hàng"], correct: 1 },
    { question: "Trong quy chuẩn setup bàn kiểu Âu, dao (Knife) được đặt ở phía nào?", options: ["Bên trái đĩa ăn", "Bên phải đĩa ăn", "Phía trên đĩa ăn", "Đặt trực tiếp lên đĩa ăn"], correct: 1 },
    { question: "Vị trí nào chịu trách nhiệm chính trong việc chạy món từ bếp ra bàn chờ (station)?", options: ["Captain", "Hostess", "Runner", "Bartender"], correct: 2 },
    { question: "Nguyên tắc L.A.S.T khi xử lý phàn nàn của khách hàng là viết tắt của?", options: ["Listen - Ask - Solve - Thank", "Look - Apologize - Smile - Talk", "Listen - Apologize - Solve - Thank", "Learn - Ask - Speak - Try"], correct: 2 },
    { question: "Kỹ năng 'Upsell' nghĩa là gì?", options: ["Mời khách dùng món có giá trị cao hơn", "Bán món ăn kèm phù hợp", "Giảm giá để khách mua nhiều hơn", "Từ chối phục vụ khách"], correct: 0 },
    { question: "Ly rượu vang đỏ thường có bầu ly như thế nào so với vang trắng?", options: ["Nhỏ hơn", "Lớn hơn và rộng hơn để rượu thở", "Cao và hẹp hơn", "Không có chân ly"], correct: 1 },
    { question: "F.O.H là viết tắt của bộ phận nào?", options: ["Full of House", "Front of House", "Back of House", "Food of House"], correct: 1 },
    { question: "Nhiệt độ phục vụ lý tưởng cho rượu vang trắng thường là bao nhiêu?", options: ["18-22°C", "0-4°C", "7-12°C", "25-30°C"], correct: 2 },
    { question: "Trong phục vụ kiểu Anh (English Service), thức ăn thường được phục vụ từ phía nào của khách?", options: ["Bên phải", "Bên trái", "Phía trước mặt", "Tùy ý"], correct: 1 },
    { question: "Thuật ngữ 'Mise en place' có nguồn gốc từ tiếng nào?", options: ["Tiếng Anh", "Tiếng Đức", "Tiếng Pháp", "Tiếng Ý"], correct: 2 },
    { question: "Dao cắt bít tết (Steak Knife) thường có đặc điểm gì?", options: ["Lưỡi phẳng không răng cưa", "Lưỡi có răng cưa sắc", "Lưỡi rất ngắn", "Lưỡi bằng nhựa"], correct: 1 },
    { question: "Khi phục vụ rượu vang, ta nên rót bao nhiêu phần của ly?", options: ["Đầy ly", "1/2 ly", "1/3 ly", "Gần đầy ly"], correct: 2 },
    { question: "Món 'Al dente' thường dùng để chỉ độ chín của món ăn nào?", options: ["Bít tết", "Mì Ý (Pasta)", "Cơm chiên", "Súp"], correct: 1 },
    { question: "Loại vang nào thường được dùng làm vang khai vị (Aperitif)?", options: ["Vang đỏ đậm", "Vang nổ (Sparkling/Champagne)", "Vang ngọt", "Vang nồng độ cao"], correct: 1 },
    { question: "Thuật ngữ 'Cover' trong báo cáo nhà hàng dùng để chỉ?", options: ["Số bàn trống", "Số lượt khách phục vụ", "Số món ăn bị hủy", "Khăn trải bàn"], correct: 1 },
    { question: "Khi bưng khay, trọng tâm của khay nên đặt ở đâu?", options: ["Đầu ngón tay", "Lòng bàn tay và các đầu ngón tay", "Cổ tay", "Khuỷu tay"], correct: 1 },
    { question: "Rượu vang đỏ thường được phục vụ ở nhiệt độ phòng, khoảng bao nhiêu?", options: ["10-12°C", "15-18°C", "20-25°C", "5-8°C"], correct: 1 },
    { question: "Thuật ngữ 'Station' trong nhà hàng nghĩa là gì?", options: ["Trạm xe buýt", "Khu vực bàn được phân công", "Quầy bar", "Kho hàng"], correct: 1 },
    { question: "Trong quy trình phục vụ, ai là người được phục vụ trước tiên?", options: ["Chủ tiệc", "Trẻ em và phụ nữ lớn tuổi", "Nam giới lớn tuổi nhất", "Người ngồi gần cửa nhất"], correct: 1 },
    { question: "Món 'Sommelier' là ai?", options: ["Đầu bếp trưởng", "Chuyên gia về rượu vang", "Người rửa bát", "Quản lý sảnh"], correct: 1 },
    { question: "Loại ly 'Flute' thường dùng để phục vụ loại đồ uống nào?", options: ["Rượu vang đỏ", "Bia", "Vang nổ/Champagne", "Nước lọc"], correct: 2 },
    { question: "Khi dọn đĩa bẩn khỏi bàn, ta nên đứng ở phía nào của khách?", options: ["Bên trái", "Bên phải", "Phía trước", "Bất kỳ phía nào"], correct: 1 },
    { question: "Thuật ngữ 'B.O.H' bao gồm những bộ phận nào?", options: ["Lễ tân, Phục vụ", "Bếp, Rửa bát, Kho", "Quản lý, Kế toán", "Bảo vệ, Tạp vụ"], correct: 1 },
    { question: "Dụng cụ 'Decanter' dùng để làm gì?", options: ["Đong rượu mạnh", "Chiết rượu vang để thở", "Lắc cocktail", "Đựng nước đá"], correct: 1 },
    { question: "Thứ tự phục vụ đồ uống tiêu chuẩn thường là?", options: ["Vang trắng -> Vang đỏ -> Vang ngọt", "Vang đỏ -> Vang trắng -> Champagne", "Vang ngọt -> Vang trắng -> Vang đỏ", "Tùy khách chọn"], correct: 0 },
    { question: "Một chai vang tiêu chuẩn có dung tích bao nhiêu?", options: ["500ml", "1000ml", "750ml", "375ml"], correct: 2 },
    { question: "Thuật ngữ 'On the rocks' khi gọi đồ uống nghĩa là gì?", options: ["Dùng với đá viên", "Dùng không đá", "Pha với nước ngọt", "Dùng nóng"], correct: 0 },
    { question: "Khi khách phàn nàn về chất lượng món ăn, bước đầu tiên nhân viên nên làm là?", options: ["Cãi lại khách", "Xin lỗi và lắng nghe", "Giao cho người khác", "Lờ đi"], correct: 1 },
    { question: "Khăn ăn (Napkin) nên được đặt ở đâu khi khách tạm thời rời bàn?", options: ["Trên bàn", "Trên ghế", "Trên đĩa bẩn", "Mang vào bếp"], correct: 1 },
    { question: "Gia vị 'Wasabi' thường đi kèm với món ăn nào?", options: ["Pizza", "Sashimi/Sushi", "Phở", "Bánh mì"], correct: 1 },
    { question: "Trong phục vụ chuyên nghiệp, ngón tay của nhân viên không bao giờ được chạm vào đâu?", options: ["Thân ly rượu", "Miệng ly và lòng đĩa ăn", "Đế ly", "Cuống ly"], correct: 1 },
    { question: "Rượu 'Chardonnay' là loại vang trắng hay vang đỏ?", options: ["Vang trắng", "Vang đỏ", "Vang hồng", "Rượu mạnh"], correct: 0 },
    { question: "Dụng cụ 'Jigger' dùng để làm gì tại quầy bar?", options: ["Mở nút chai", "Đong định lượng chất lỏng", "Nghiền trái cây", "Lọc đá"], correct: 1 },
    { question: "Món 'Garnish' trong món ăn hay đồ uống là gì?", options: ["Thành phần chính", "Phần trang trí", "Nước xốt", "Gia vị cay"], correct: 1 },
    { question: "Khi phục vụ trà hoặc cà phê, quai tách nên hướng về phía nào của khách?", options: ["Phía bên trái (hướng 9 giờ)", "Phía bên phải (hướng 3-4 giờ)", "Phía trước mặt", "Không quan trọng"], correct: 1 },
    { question: "Loại vang 'Cabernet Sauvignon' nổi tiếng là?", options: ["Vang trắng nhẹ", "Vang đỏ đậm đà", "Vang sủi", "Vang ngọt"], correct: 1 },
    { question: "Thuật ngữ 'Void' trên máy POS nghĩa là gì?", options: ["In hóa đơn", "Tạm tính", "Hủy món đã nhập", "Chuyển bàn"], correct: 2 },
    { question: "Khi khách làm rơi nĩa xuống sàn, nhân viên nên làm gì?", options: ["Lấy nĩa đó lên lau sạch trả khách", "Mang nĩa mới ra trước rồi mới nhặt nĩa cũ", "Bảo khách tự nhặt", "Lờ đi"], correct: 1 },
    { question: "Món 'Medium Rare' cho bít tết có nghĩa là?", options: ["Chín kỹ", "Tái hồng (ấm ở giữa, đỏ bên trong)", "Sống hoàn toàn", "Chín vừa"], correct: 1 },
    { question: "Phục vụ kiểu Pháp (French Service) có đặc điểm gì?", options: ["Khách tự phục vụ", "Nhân viên chế biến/hoàn thiện món tại bàn khách", "Bưng đĩa ra là xong", "Đồ ăn để sẵn trên bàn"], correct: 1 },
    { question: "Dụng cụ 'Crumber' dùng để làm gì?", options: ["Cắt bánh mì", "Gạt vụn bánh mì trên bàn", "Mở nắp chai", "Đựng tiêu"], correct: 1 },
    { question: "Rượu 'Sparkling Wine' khác 'Champagne' ở điểm nào?", options: ["Màu sắc", "Giá tiền", "Vùng sản xuất (Champagne chỉ từ vùng Champagne, Pháp)", "Độ cồn"], correct: 2 },
    { question: "Khi rót nước lọc, nhân viên nên rót bao nhiêu?", options: ["Đầy tràn", "Cách miệng ly khoảng 1-2cm", "Nửa ly", "Tùy khách nhắc"], correct: 1 },
    { question: "Tại sao phải 'Polishing' dụng cụ (ly, dao, nĩa)?", options: ["Để làm nóng", "Để loại bỏ vết vân tay và vết nước khô", "Để làm sắc dao", "Để khử mùi"], correct: 1 },
    { question: "Món 'Appetizer' là gì?", options: ["Món chính", "Món khai vị", "Món tráng miệng", "Đồ uống tiêu hóa"], correct: 1 },
    { question: "Hành động 'Table Turn' nghĩa là gì?", options: ["Xoay bàn cho khách", "Lượt khách mới sử dụng cùng một bàn", "Dọn bàn nhanh", "Lật khăn trải bàn"], correct: 1 },
    { question: "Loại vang 'Rosé' có màu gì?", options: ["Đỏ", "Trắng", "Hồng", "Vàng rơm"], correct: 2 },
    { question: "Khi khách gọi món mà bếp báo '86', bạn nên làm gì?", options: ["Cứ ghi order rồi tính sau", "Báo ngay với khách và gợi ý món tương tự", "Im lặng", "Bảo khách tự chọn món khác"], correct: 1 },
    { question: "Nhiệt độ tối thiểu để giữ thực phẩm nóng an toàn là bao nhiêu?", options: ["40°C", "60°C", "100°C", "80°C"], correct: 1 },
    { question: "Trong quầy bar, 'Shaker' dùng để làm gì?", options: ["Khuấy nhẹ đồ uống", "Lắc để trộn và làm lạnh đồ uống", "Đựng đá", "Ép trái cây"], correct: 1 },
    { question: "Món 'Condiment' nghĩa là gì?", options: ["Món chính", "Đồ gia vị ăn kèm (tương ớt, muối, tiêu...)", "Tráng miệng", "Đồ uống"], correct: 1 },
    { question: "Khi dọn ly rượu vang, ta nên cầm ở đâu?", options: ["Bầu ly", "Miệng ly", "Chân/Cuống ly", "Cầm lòng bàn tay"], correct: 2 },
    { question: "Dấu hiệu 'X' tạo bởi dao và nĩa trên đĩa của khách nghĩa là?", options: ["Đã ăn xong", "Chưa ăn xong (tạm dừng)", "Món ăn quá tệ", "Muốn gọi món thêm"], correct: 1 },
    { question: "Thuật ngữ 'Voucher' là gì?", options: ["Hóa đơn đỏ", "Phiếu giảm giá/thanh toán", "Thẻ nhân viên", "Menu nhỏ"], correct: 1 },
    { question: "Ly 'Tumbler' thường dùng cho loại đồ uống nào?", options: ["Rượu vang", "Nước lọc, nước trái cây, soda", "Champagne", "Cà phê nóng"], correct: 1 },
    { question: "Khi giới thiệu thực đơn, nhân viên nên đứng như thế nào?", options: ["Khoanh tay trước ngực", "Đứng thẳng, tay để sau lưng hoặc đan phía trước", "Dựa vào tường", "Ngồi xuống với khách"], correct: 1 },
    { question: "Thành phần chính của rượu vang là gì?", options: ["Lúa mạch", "Nho", "Gạo", "Khoai tây"], correct: 1 },
    { question: "Tại sao nhân viên nhà hàng không nên dùng nước hoa quá nồng?", options: ["Tốn tiền", "Làm át đi mùi hương của món ăn và rượu vang", "Gây hắt xì cho đầu bếp", "Quy định để tiết kiệm"], correct: 1 },
    { question: "Khoảng cách an toàn giữa các ghế tại bàn tiệc nên là bao nhiêu?", options: ["10cm", "30-50cm", "100cm", "Sát nhau"], correct: 1 },
    { question: "Mục tiêu cuối cùng của ngành Hospitality là gì?", options: ["Kiếm tiền", "Sự hài lòng và trải nghiệm của khách hàng", "Làm món ăn đẹp", "Xây dựng nhà hàng to"], correct: 1 },
  ];

  const handleStart = () => {
    setGameState('playing');
    setCurrentQuestion(0);
    setScore(0);
    setShowFeedback(false);
    setSelectedAnswer(null);
  };

  const handleAnswerClick = (index) => {
    if (showFeedback) return;

    setSelectedAnswer(index);
    setShowFeedback(true);
    
    if (index === questions[currentQuestion].correct) {
      setIsCorrect(true);
      setScore(score + 1); 
    } else {
      setIsCorrect(false);
    }

    setTimeout(() => {
      if (currentQuestion < questions.length - 1) {
        setCurrentQuestion(currentQuestion + 1);
        setShowFeedback(false);
        setSelectedAnswer(null);
      } else {
        setGameState('result');
      }
    }, 1200);
  };

  const StartScreen = () => (
    <div className="flex flex-col items-center justify-center h-full text-center space-y-6 animate-fadeIn p-6">
      <div className="bg-orange-100 p-8 rounded-full text-orange-600 mb-4 shadow-inner ring-4 ring-orange-50">
        <HelpCircle size={80} />
      </div>
      <div className="space-y-2">
        <h1 className="text-4xl md:text-5xl font-black text-slate-800 tracking-tight">
          Master of <span className="text-orange-600 font-serif italic">Hospitality</span>
        </h1>
        <p className="text-slate-500 font-medium text-lg uppercase tracking-widest">Thử thách 60 câu hỏi chuyên sâu</p>
      </div>
      <p className="text-slate-500 max-w-md text-lg leading-relaxed">
        Bộ trắc nghiệm toàn diện về nghiệp vụ F&B. Bạn cần đạt trên <strong>50/60</strong> để trở thành Chuyên gia!
      </p>
      <button 
        onClick={handleStart}
        className="group bg-orange-600 text-white px-10 py-5 rounded-2xl font-bold text-2xl hover:bg-orange-700 transition-all shadow-xl hover:scale-105 flex items-center gap-3 active:scale-95"
      >
        <Play fill="white" size={24} />
        Bắt đầu thi
      </button>
    </div>
  );

  const QuizScreen = () => {
    const question = questions[currentQuestion];
    const progress = ((currentQuestion + 1) / questions.length) * 100;

    return (
      <div className="w-full max-w-3xl mx-auto p-4 md:p-0 animate-fadeIn">
        <div className="mb-8">
          <div className="flex justify-between items-end text-sm font-bold text-slate-500 mb-3 uppercase tracking-tighter">
            <span className="flex items-center gap-2">
              <span className="text-orange-600 text-xl">#{currentQuestion + 1}</span> / {questions.length}
            </span>
            <span className="bg-slate-200 px-3 py-1 rounded-lg text-slate-700">Điểm: {score}</span>
          </div>
          <div className="h-2 w-full bg-slate-200 rounded-full overflow-hidden shadow-inner">
            <div 
              className="h-full bg-gradient-to-r from-orange-400 to-orange-600 transition-all duration-300 ease-out" 
              style={{ width: `${progress}%` }}
            ></div>
          </div>
        </div>

        <div className="bg-white rounded-[2rem] shadow-2xl p-6 md:p-12 border border-slate-100 relative min-h-[500px] flex flex-col justify-center">
          <h2 className="text-2xl md:text-3xl font-bold text-slate-800 mb-10 leading-snug">
            {question.question}
          </h2>

          <div className="grid grid-cols-1 gap-4">
            {question.options.map((option, index) => {
              let btnClass = "w-full text-left p-5 rounded-2xl border-2 font-semibold transition-all duration-150 flex justify-between items-center group relative overflow-hidden ";
              
              if (showFeedback) {
                if (index === question.correct) {
                  btnClass += "border-green-500 bg-green-50 text-green-700 scale-[1.02] z-10 shadow-lg shadow-green-100";
                } else if (index === selectedAnswer) {
                  btnClass += "border-red-500 bg-red-50 text-red-700 opacity-90";
                } else {
                  btnClass += "border-slate-50 text-slate-300 opacity-40";
                }
              } else {
                btnClass += "border-slate-100 hover:border-orange-500 hover:bg-orange-50 text-slate-600 hover:text-orange-800 hover:translate-x-2";
              }

              return (
                <button
                  key={index}
                  onClick={() => handleAnswerClick(index)}
                  disabled={showFeedback}
                  className={btnClass}
                >
                  <span className="flex gap-4">
                    <span className={`w-7 h-7 flex items-center justify-center rounded-lg text-sm ${showFeedback && index === question.correct ? 'bg-green-500 text-white' : 'bg-slate-100 text-slate-400'}`}>
                      {String.fromCharCode(65 + index)}
                    </span>
                    {option}
                  </span>
                  {showFeedback && index === question.correct && <CheckCircle size={22} className="text-green-600" />}
                  {showFeedback && index === selectedAnswer && index !== question.correct && <XCircle size={22} className="text-red-500" />}
                </button>
              );
            })}
          </div>
        </div>
      </div>
    );
  };

  const ResultScreen = () => {
    const percentage = (score / questions.length) * 100;
    
    let message = "";
    let icon = null;
    let colorClass = "";

    if (percentage >= 90) {
      message = "Cấp độ: LEGENDARY! Bạn là một Quản lý Nhà hàng thực thụ.";
      icon = <Trophy size={100} className="text-yellow-500" />;
      colorClass = "text-yellow-600 bg-yellow-100";
    } else if (percentage >= 70) {
      message = "Cấp độ: PROFESSIONAL! Kiến thức của bạn rất vững chắc.";
      icon = <Star size={100} className="text-blue-500" />;
      colorClass = "text-blue-600 bg-blue-100";
    } else if (percentage >= 50) {
      message = "Cấp độ: COMPETENT! Bạn đủ khả năng làm việc ở nhà hàng cao cấp.";
      icon = <CheckCircle size={100} className="text-green-500" />;
      colorClass = "text-green-600 bg-green-100";
    } else {
      message = "Cấp độ: NOVICE! Bạn cần đọc lại 'Sổ tay F&B' nhiều hơn.";
      icon = <RefreshCcw size={100} className="text-slate-400" />;
      colorClass = "text-slate-600 bg-slate-100";
    }

    return (
      <div className="flex flex-col items-center justify-center h-full text-center space-y-10 animate-fadeIn p-6">
        <div className={`p-10 rounded-[3rem] shadow-2xl ${colorClass} animate-bounce`}>
          {icon}
        </div>
        
        <div className="space-y-4">
          <h2 className="text-6xl font-black text-slate-800">{score} <span className="text-3xl text-slate-400 font-medium">/ {questions.length}</span></h2>
          <div className="h-1.5 w-48 bg-slate-200 mx-auto rounded-full overflow-hidden">
            <div className="h-full bg-orange-600" style={{ width: `${percentage}%` }}></div>
          </div>
          <p className="text-2xl font-bold text-slate-700 max-w-md mx-auto">{message}</p>
        </div>

        <button 
          onClick={handleStart}
          className="flex items-center gap-3 bg-slate-800 text-white px-10 py-4 rounded-2xl font-bold text-xl hover:bg-black transition shadow-2xl active:scale-95"
        >
          <RefreshCcw size={24} />
          Thi lại lần nữa
        </button>
      </div>
    );
  };

  return (
    <div className="min-h-screen bg-[#f8fafc] font-sans flex flex-col selection:bg-orange-200">
      <header className="bg-white/80 backdrop-blur-md sticky top-0 z-50 border-b border-slate-100 py-5 px-8 flex justify-between items-center shadow-sm">
        <div className="flex items-center gap-2">
          <div className="bg-orange-600 text-white w-10 h-10 flex items-center justify-center rounded-xl font-black shadow-lg shadow-orange-200">FB</div>
          <h1 className="text-xl font-black text-slate-800 tracking-tight hidden md:block">
            ADVANCED QUIZ
          </h1>
        </div>
        <div className="flex items-center gap-4 text-slate-500 font-bold text-sm">
          <Timer size={18} className="text-orange-500" />
          <span>EST. 15 MINS</span>
        </div>
      </header>

      <main className="flex-grow flex items-center justify-center py-10">
        {gameState === 'start' && <StartScreen />}
        {gameState === 'playing' && <QuizScreen />}
        {gameState === 'result' && <ResultScreen />}
      </main>

      <footer className="py-8 text-center">
        <p className="text-slate-400 font-semibold tracking-widest text-xs uppercase">
          © 2024 • Training Material • F&B Professional Series
        </p>
      </footer>
    </div>
  );
};

export default App;
