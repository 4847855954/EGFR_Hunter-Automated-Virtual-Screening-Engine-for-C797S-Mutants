# EGFR_Hunter-Automated-Virtual-Screening-Engine-for-C797S-Mutants:
EGFR_Hunter 是一套專為對抗 EGFR C797S 耐藥突變設計的開源 CADD/AIDD 自動化流水線
# Key Features:
/AI-Powered Fast Screening: 整合 2054 維 ECFP4 特徵工程與 XGBoost QSAR 模型，數秒內預測活性標度 (pIC50)。  

/Physics-Based 3D Validation: 自動調用 OpenBabel & AutoDock Vina，針對 C797S 晶體口袋 (6LUD) 進行結合能預測 (Delta G)。 

/Zero-Setup & Robust: 內建自癒式依賴套件安裝與結構 Sanitize 機制，完全不懼環境重置。 

/In-Browser 3D Viewer: 整合 py3Dmol，免安裝桌面版 PyMOL 即可查看分子打靶姿勢。  

# [目前基礎：v1.0 乾實驗引擎]
       │
       ├─── 1. 動態物理模擬 (MD & MM/PBSA) ───> 補足靜態對接的假陽性
       ├─── 2. 生成式 AI (De Novo Design) ───> 擺脫已知分子庫限制
       ├─── 3. 藥物成藥性 (ADMET & SA Score) ─> 避免設計出「無法合成/毒性爆表」的分子
       ├─── 4. 專利查重 (Patent Novelty) ────> 確保智慧財產權 (IP) 完全原創
       └─── 5. 濕實驗轉譯語文 (In Vitro) ─────> 建立與生化/細胞實驗室對接的 Protocol

================================================================================
📋 EGFR_Hunter 流水線升級與知識補足清單 (v2.0 研發藍圖)
================================================================================

1. 動態物理與口袋柔性（從「靜態對接」走向「分子動力學 MD」）
現狀缺口：AutoDock Vina 採用的是「硬性/半硬性受體」假設。但真實人體內的 C797S 蛋白是處於水溶液環境且不斷震盪的，水分子（Hydration Shell）甚至會介導關鍵的氫鍵網絡。  
需補足知識：
分子動力學模擬（Molecular Dynamics, MD）：如何利用 OpenMM 或 GROMACS 在 Python 中執行 50～100 ns 的動態模擬，觀察小分子是否會在體溫震盪下脫落。
自由能精算（MM/PBSA or MM/GBSA）：比 Vina 更準確地計算動態結合自由能 ΔG。

2. 化學空間主動探索（從「篩選已知」走向「De Novo 分子生成」）
現狀缺口：我們目前是輸入「現成的 SMILES 清單」讓 AI 評分。這依然受限於我們輸入了什麼。  
需補足知識：
生成式 AI 模型（如 REINVENT、Pocket2Mol、DiffDock）：如何設定條件（如：「必須保留與 Met793 的氫鍵」+「對 C797S 口袋親和力 ΔG < -9.0 kcal/mol」），讓 AI 自動為 C797S 口袋從零畫出（De Novo Generation）數萬個全新的化學結構。

3. 成藥性與藥化過濾（ADMET & 合成難易度 SA Score）
現狀缺口：AI 預測活性高（pIC50 > 8.0）且對接分數極佳（ΔG < -10.0 kcal/mol）的分子，在現實世界中可能極度難以合成，或者肝毒性/心臟毒性爆表。
需補足知識：
SA Score (Synthetic Accessibility Score)：如何在 RDKit 中評估分子的有機合成難易度（確保藥化師做得出來）。
PAINS 過濾器 (Pan-Assay Interference Compounds)：自動剔除化學結構上的「偽陽性陷阱（如易活化的親核性活性基團）」。
ADMET 預測：預測人體腸道吸收（HIA）、血腦屏障滲透（BBB）、CYP450 酵素代謝穩定性與 hERG 心臟毒性。

4. 專利檢索與智慧財產權查重（Patent Novelty Engine）
現狀缺口：如果 AI 篩出一個好分子，但幾年前 Astra Zeneca 或 Blueprint Medicines 已經申請過相關母核專利，那這個分子就毫無商業與學術原創價值。
需補足知識：
專利相似度 API 串接：串接 SureChEMBL、PubChem Patents 或 SciFinder，利用 Tanimoto 結構相似度演算法（Tanimoto Similarity < 0.7），自動檢查 Hit 分子是否位於專利空白區。

5. 濕實驗轉譯與數據語文（In Vitro Validation Protocol）
現狀缺口：當我們要拿這份報告去尋求清華/台大/中研院的生化實驗室合作，或是向投資人簡報時，需要將乾實驗數據翻譯成濕實驗語言。
需補足知識：
熟悉常用生化驗證指標：如 IC50 激酶抑制試驗 (Z'-LYTE / HTRF)、細胞增殖抑制實驗 (Ba/F3 C797S 工程株)，以及 表面電漿共振 (SPR) 測量 Kd 結合常數 的對應關係。
