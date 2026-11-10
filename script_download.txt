const duas = [
"اللهم اغفر لهنادي علي محمد وارحمها، وعافها واعفُ عنها، وأكرم نُزلها، ووسّع مُدخلها، ونوّر قبرها، واجعل قبرها روضةً من رياض الجنة.",
"اللهم آنس وحشتها، وآمن روعتها، وثبّتها عند السؤال، واجعل الجنة مستقرّها ومأواها.",
"اللهم ارفع درجتها في المهديين، واخلفها في أهلها في الغابرين، واغفر لنا ولها يا رب العالمين.",
"اللهم اجعل لها نوراً في قبرها، واجعل الجنة دارها وقرارها."
];
let duaIndex=0,count=0;
const countEl=document.getElementById("count");
const zikrEl=document.getElementById("zikr");
const toastEl=document.getElementById("toast");
function toast(message){
  toastEl.textContent=message;toastEl.classList.add("show");
  clearTimeout(window.toastTimer);
  window.toastTimer=setTimeout(()=>toastEl.classList.remove("show"),2200);
}
function shareText(text,title){
  if(navigator.share){navigator.share({title,text,url:location.href}).catch(()=>{});}
  else if(navigator.clipboard){navigator.clipboard.writeText(text+"\n"+location.href).then(()=>toast("تم نسخ الرابط، يمكنك مشاركته الآن")).catch(()=>toast("انسخ رابط الموقع من شريط العنوان"));}
  else toast("انسخ رابط الموقع من شريط العنوان");
}
document.getElementById("nextDua").addEventListener("click",()=>{
  duaIndex=(duaIndex+1)%duas.length;
  document.getElementById("duaText").textContent=duas[duaIndex];
});
document.getElementById("shareDua").addEventListener("click",()=>{
  shareText(document.getElementById("duaText").textContent,"دعاء للمرحومة هنادي علي محمد");
});
document.getElementById("shareSite").addEventListener("click",()=>{
  shareText("صدقة جارية على روح المرحومة هنادي علي محمد. لا تنسوها من صالح دعائكم.","صدقة جارية لهنادي");
});
document.getElementById("countBtn").addEventListener("click",()=>{
  count++;countEl.textContent=count;
  if(count%33===0)toast("أحسنت، تقبّل الله منك");
});
document.getElementById("resetBtn").addEventListener("click",()=>{
  count=0;countEl.textContent=count;
});
document.querySelectorAll(".zikr-option").forEach(button=>{
  button.addEventListener("click",()=>{
    document.querySelectorAll(".zikr-option").forEach(b=>b.classList.remove("active"));
    button.classList.add("active");zikrEl.textContent=button.dataset.zikr;
  });
});
