# Thai Government Lottery Results

Every draw of the Thai Government Lottery since 1 March 2010 (B.E. 2553), as plain CSV files. Maintained by [HuayBase](https://huaybase.com) and updated automatically after each draw.

Want statistics without writing code? HuayBase has [frequent and long-absent numbers](https://huaybase.com/statistics/hot-cold), [digit statistics with a randomness test](https://huaybase.com/statistics/digits) and a [tool to look up your own number](https://huaybase.com/my-number), all in Thai.

**ภาษาไทย:** ผลสลากกินแบ่งรัฐบาลทุกงวดตั้งแต่ 1 มีนาคม 2553 เป็นไฟล์ CSV ดูแลโดย [HuayBase](https://huaybase.com) และอัปเดตอัตโนมัติหลังมีผลงวดใหม่ อ่านสรุปภาษาไทยได้[ด้านล่าง](#ภาษาไทย) หรือที่[หน้าดาวน์โหลดข้อมูล](https://huaybase.com/dataset)

อยากดูสถิติโดยไม่ต้องคำนวณเอง ดูได้ที่[สถิติหวย](https://huaybase.com) [เลขออกบ่อย / ไม่ออกนาน](https://huaybase.com/statistics/hot-cold) [สถิติหลักสิบ หลักหน่วย](https://huaybase.com/statistics/digits) และ[เลขของฉันเคยถูกไหม](https://huaybase.com/my-number)

## Files

| File | One row per | Contents |
|---|---|---|
| `draws.csv` | draw | First prize, its two neighbours, three-digit prizes, last two digits, link to the official result sheet |
| `prizes.csv` | prize number | Every prize of every draw, including the second to fifth prizes |
| `notes.json` | | Draws held on another day, and scheduled draws that were cancelled, with sources |

## Quick start

Read the numbers as text. They can start with a zero (`006082`, `04`), and a spreadsheet that opens a CSV directly will drop it. In Excel, use Data → From Text/CSV and set the number columns to Text.

```python
import pandas as pd

prizes = pd.read_csv("prizes.csv", dtype={"number": str})
draws = pd.read_csv("draws.csv", dtype=str)
```

## Columns

### `draws.csv`

| Column | Meaning |
|---|---|
| `date` | Draw date as published by the Government Lottery Office (GLO), Gregorian |
| `date_be` | The same date in the Buddhist era |
| `actual_draw_date` | The day the drawing happened, only where it differs from `date` |
| `first` | First prize |
| `near_first` | The two numbers next to the first prize |
| `front3` | Front three digits. Empty before 1 September 2015 |
| `back3` | Last three digits |
| `back2` | Last two digits |
| `pdf_url` | Official result sheet |
| `checked_against_pdf` | `true` if this draw was checked against that sheet |

Cells with several numbers separate them with a space.

### `prizes.csv`

| Column | Meaning |
|---|---|
| `date` | Draw date, Gregorian |
| `prize` | Prize type, see below |
| `number` | The winning number |
| `amount_baht` | Prize per ticket in baht. Empty before 1 September 2017 |

| `prize` | Prize | Numbers per draw |
|---|---|---|
| `first` | รางวัลที่ 1 | 1 |
| `near_first` | รางวัลข้างเคียงรางวัลที่ 1 | 2 |
| `second` | รางวัลที่ 2 | 5 |
| `third` | รางวัลที่ 3 | 10 |
| `fourth` | รางวัลที่ 4 | 50 |
| `fifth` | รางวัลที่ 5 | 100 |
| `front3` | รางวัลเลขหน้า 3 ตัว | 2 (none before 1 September 2015) |
| `back3` | รางวัลเลขท้าย 3 ตัว | 2 (4 before 1 September 2015) |
| `back2` | รางวัลเลขท้าย 2 ตัว | 1 |

Rows are sorted by date. Within a draw and a prize, numbers keep the order of the source.

### `notes.json`

`draws` holds notes by draw date. `suspended` lists scheduled draws that were cancelled, so they have no row in the CSV files. Each entry links to its source.

## Where the data comes from

Results come from GLO's own result system, starting with the first draw it makes available.

- **Checked on every draw:** the number of prizes for the structure of that time, the number of digits, the first prize's neighbours, and the main prizes against GLO's yearly list.
- **Spot-checked against the official sheet:** a sample of draws was compared with the official PDF, and every number was found on the sheet. Those draws have `checked_against_pdf` set to `true`. The others have not been compared sheet by sheet.
- **Never filled in:** nothing is guessed. A number the source lists twice within a prize stays as published.
- **Amounts:** left empty before 1 September 2017, because the source reports today's amounts for older draws too.
- **Dates:** most draws are on the 1st and 16th, but not all. The 1 April 2020 draw was held on 16 May 2020.

The full method is on the [HuayBase methodology page](https://huaybase.com/methodology) (in Thai). A GitHub Action checks huaybase.com once a day and commits when anything changes. Found an error? Open an issue or use the [contact page](https://huaybase.com/contact).

## This is not an official source

Only results from [GLO](https://www.glo.or.th) can be used to claim a prize, so check the official result sheet first. HuayBase is not part of GLO, and GLO does not endorse this dataset.

Each draw is independent. Past results do not change the chance of any number in a future draw, and this dataset does not predict anything.

## License and credit

[CC BY 4.0](LICENSE). You may reuse and adapt the files, also commercially, if you give credit and say what you changed. The license covers what HuayBase made: the compilation, file format, documentation and notes. The results themselves are facts published by GLO.

Please credit with links (`nofollow` is fine):

```
Data: HuayBase https://huaybase.com Dataset: https://huaybase.com/dataset (CC BY 4.0)
```

## ภาษาไทย

- **`draws.csv`** 1 แถวต่อ 1 งวด มีรางวัลที่ 1 รางวัลข้างเคียง เลข 3 ตัว เลขท้าย 2 ตัว และลิงก์ใบตรวจผลทางการ
- **`prizes.csv`** 1 แถวต่อ 1 เลขรางวัล ครบทุกรางวัล รวมรางวัลที่ 2 ถึงรางวัลที่ 5
- **`notes.json`** งวดที่ออกรางวัลคนละวันกับวันที่ของงวด และงวดที่งดออก พร้อมแหล่งอ้างอิง

**เลข 0 นำหน้า:** เลขรางวัลบางเลขขึ้นต้นด้วย 0 ถ้าดับเบิลคลิกเปิดใน Excel เลข 0 จะหาย ให้นำเข้าผ่าน Data → From Text/CSV แล้วตั้งคอลัมน์เลขเป็น Text

**ที่มาของข้อมูล:** ผลรางวัลมาจากระบบของสำนักงานสลากกินแบ่งรัฐบาล ทุกงวดผ่านการตรวจอัตโนมัติ และสุ่มเทียบกับใบตรวจผล PDF บางงวด (`checked_against_pdf` เป็น `true`) งวดอื่นยังไม่ได้เทียบทีละใบ ไม่มีการเดาหรือเติมข้อมูลที่ขาด

**ไม่ใช่แหล่งทางการ:** ผลที่ใช้ขึ้นเงินรางวัลได้คือผลจากสำนักงานสลากกินแบ่งรัฐบาลเท่านั้น HuayBase ไม่ได้เป็นส่วนหนึ่งของสำนักงาน และสำนักงานไม่ได้รับรองชุดข้อมูลนี้ ผลแต่ละงวดเป็นอิสระต่อกัน สถิติในอดีตไม่ได้ทำให้โอกาสของเลขใดในงวดถัดไปสูงขึ้นหรือต่ำลง

**สัญญาอนุญาต:** [CC BY 4.0](LICENSE) นำไปใช้ต่อ ดัดแปลง หรือใช้เชิงพาณิชย์ได้ โดยให้เครดิตและบอกว่าแก้ไขอะไรบ้าง สัญญานี้ครอบคลุมส่วนที่ HuayBase จัดทำเอง ส่วนผลรางวัลเป็นข้อเท็จจริงที่สำนักงานสลากกินแบ่งรัฐบาลประกาศ

ข้อความให้เครดิต (ถ้าเป็นเว็บไซต์ ขอให้ทำ URL เป็นลิงก์ จะใส่ nofollow หรือไม่ก็ได้):

```
ข้อมูลจาก HuayBase https://huaybase.com ชุดข้อมูล: https://huaybase.com/dataset (CC BY 4.0)
```
