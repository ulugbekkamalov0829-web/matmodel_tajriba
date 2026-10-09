# 2-tajriba ishi: taqsimot qonuni

Matematik modellashtirish fanidan 2-tajriba ishining 25 ta topshirig'i uchun yechimlar sayti.
Har kim o'z topshirig'ining raqamini (1–25) yoki kategoriyasini (A–E) tanlaydi, sayt yechimni
namunadagi jadval ko'rinishida chiqaradi va Excel faylini formulalari bilan yuklab beradi.

Sayt manzili (GitHub Pages yoqilgandan keyin): `https://ulugbekkamalov0829-web.github.io/matmodel_tajriba/`

## Qanday ishlatiladi

1. Saytni oching.
2. Jadvaldan o'z topshirig'ingiz raqamini bosing yoki maydonga raqamni yozing (masalan `7`).
   Butun kategoriya kerak bo'lsa, ustun sarlavhasini bosing yoki harfini yozing (masalan `C`).
3. Yechim jadvali chiqadi: parametrlar, taqsimot qonuni, M(X), D(X), σ(X) va nazariy javob.
4. "Excel faylini yuklab olish" tugmasi `.xlsx` faylni beradi. Fayldagi kataklar formulalar bilan
   to'ldirilgan (`COMBIN`, `SUMPRODUCT`, `SQRT`), shuning uchun uni Excelda ochib tekshirish mumkin.

Havolani to'g'ridan-to'g'ri yuborish ham mumkin: manzil oxiriga `#7` qo'shilsa 7-topshiriq,
`#C` qo'shilsa C kategoriya ochiladi.

## Kategoriyalar

| Kategoriya | Topshiriqlar | Mavzu |
|---|---|---|
| A | 1–5 | Diskret tasodifiy miqdorni modellashtirish |
| B | 6–10 | Ishlab chiqarish va texnik jarayonlar |
| C | 11–15 | Axborot texnologiyalari va raqamli tizimlar |
| D | 16–20 | Qishloq xo'jaligi va tabiiy jarayonlar |
| E | 21–25 | Murakkabroq modellashtirish topshiriqlari |

## Yechish usuli

Barcha topshiriqlarda n ta mustaqil tajriba o'tkaziladi va har birida hodisa bir xil p ehtimol
bilan ro'y beradi. Shuning uchun X binomial taqsimotga bo'ysunadi:

```
P(X = k) = C(n; k) · p^k · q^(n−k),   q = 1 − p,   k = 0, 1, …, n
M(X) = Σ k·P(X=k) = n·p
D(X) = M(X²) − [M(X)]² = n·p·q
σ(X) = √D(X)
```

Excel faylida shu hisoblar quyidagi formulalar bilan yozilgan (n — `B4`, p — `D4`, q — `B5` katakda;
kataklar manzili n = 5 bo'lgan topshiriq misolida):

| Kattalik | Formula |
|---|---|
| C(n; k) | `=COMBIN($B$4;A8)` |
| P(X = k) | `=B8*$D$4^A8*$B$5^($B$4-A8)` |
| M(X) | `=SUMPRODUCT(A8:A13;C8:C13)` |
| M(X²) | `=SUMPRODUCT(A8:A13^2;C8:C13)` |
| D(X) | `=C18-C17^2` |
| σ(X) | `=SQRT(C19)` |

Excelning ruscha talqinida funksiya nomlari o'zi tarjima bo'lib ko'rinadi
(`ЧИСЛКОМБ`, `СУММПРОИЗВ`, `КОРЕНЬ`).

Alohida holatlar:

- 21-topshiriq: 20 foiz = 0,2, ya'ni p = 0,2.
- 22-topshiriq: nazoratlar mustaqil, shuning uchun p = 0,9 · 0,8 = 0,72.
- 24-topshiriq: P(X ≤ 2) = P(X=0) + P(X=1) + P(X=2).
- 25-topshiriq: P(X ≥ 2) = 1 − P(X=0) − P(X=1), oxirida natija izohi beriladi.

## Fayllar

| Fayl | Vazifasi |
|---|---|
| `index.html` | Butun sayt: ko'rinish (CSS), topshiriqlar ro'yxati, hisoblash va Excel fayl yaratish (JavaScript) |
| `README.md` | Shu tavsif |

Sayt hech qanday tashqi kutubxona yoki serverga bog'liq emas, `index.html` ni kompyuterda
ikki marta bosib ochsangiz ham ishlaydi.

## Topshiriq qo'shish yoki o'zgartirish

`index.html` ichidagi `TASKS` ro'yxatiga yangi yozuv qo'shiladi:

```js
{ id: 26, cat: "E", title: "Yangi topshiriq", n: 5, p: 0.3,
  text: "Topshiriq sharti ...",
  ev: "sanalayotgan hodisa",            // izoh ustunida chiqadi: "2 ta sanalayotgan hodisa"
  pl: "Hodisa ro'y berish ehtimoli",    // p ning nomi
  ql: "Hodisa ro'y bermaslik ehtimoli", // q ning nomi
  x: "5 ta tajribada hodisa ro'y berishlar soni" }
```

Mavjud topshiriqning sonlari o'zgarsa, faqat `n` va `p` ni almashtirish kifoya, jadval va Excel
fayli o'zi qayta hisoblanadi.

## GitHubga yuklash

1. [github.com](https://github.com) da akkauntga kiring, yuqori o'ngdagi **+** → **New repository**.
2. Nom: `matmodel_tajriba`, tur: **Public**, **Create repository**.
3. Ochilgan sahifada **uploading an existing file** havolasini bosing, `index.html` va `README.md`
   fayllarini oynaga tashlang, pastda **Commit changes**.
4. **Settings** → **Pages** → **Branch** ostida `main` va `/ (root)` ni tanlang, **Save**.
5. Bir-ikki daqiqadan keyin sayt `https://ulugbekkamalov0829-web.github.io/matmodel_tajriba/` manzilida ochiladi.
   Shu havolani guruhga yuboring.

Git o'rnatilgan bo'lsa, 3-qadam o'rniga terminalda:

```bash
cd matmodel_tajriba
git init -b main
git add index.html README.md
git commit -m "2-tajriba ishi: taqsimot qonuni sayti"
git remote add origin https://github.com/ulugbekkamalov0829-web/matmodel_tajriba.git
git push -u origin main
```

Guruhdoshlar ham o'zgartirish kirita olishi uchun: **Settings** → **Collaborators** → **Add people**.
