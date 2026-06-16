# All Digital Phase Locked Loop (ADPLL)

## PROBLEM STATEMENT

All-Digital Phase-Locked Loop（ADPLL）的一般架構如圖 1.所示。首先，相位和頻率檢測器（PFD）比較REF_CLK和Out_divM 之間的相位和頻率誤差。
然後，它輸出一個控制訊號給PLL控制器，以更新數位控制振盪器（DCO）的輸出頻率，以追蹤REF_CLK。最後，當ADPLL 被鎖定時，它轉入相位和頻率維持模式，繼續跟蹤REF_CLK的相位和頻率。

<div align = center>
<img width="995" height="425" alt="image" src="https://github.com/user-attachments/assets/51f8dcb7-9944-4c76-b241-1841ce8922fb" />
</div>

## METHODOLOGY 

本專題的主題為設計一個全數位相位鎖定迴路（ADPLL），並使用 ADE-L進行模擬驗證，包括模擬類比和混合模式。以下表1.提供系統I/O定義：

<div align = center>
<img width="1037" height="405" alt="image" src="https://github.com/user-attachments/assets/9186ddd5-142b-4631-a15c-505d9d336dbe" />
</div>

在這次的架構實作中，我們將分為兩個階段進行：首先，將利用RTL進行PLL 功能的實現 **<ins>(Demo1)</ins>**，整合和實現相位鎖定迴路的核心功能。其次，將進行ADE-L 模擬，其中相位和頻率檢測器（PFD）以及數位控制振盪器（DCO）將使
用Spice 電路進行模擬 **<ins>(Demo2)</ins>** 。這樣的分階段方法確保我們能夠先專注於數位邏輯的實現，然後再進一步驗證加入Spice電路的情形，以確保整體架構的正確性和性能。 

## METHODOLOGY (Loop Filter)

此外，考量到PLL中DCO的Control Code震盪情形，希望能夠在鎖定時的抖動最小化以及維持追蹤。在Controller中參考了文獻”Method And Apparatus For Performing Phase Acquisition In An All Digital Phase Lock Loop”相關設計。

其主要精神在於透過紀錄baseline的頻率和counter機制: 

- 假設control code 每次遞增counter會進行+1，遞減則反之。 
- counter=4，紀錄相位的領先/落後情形並調整baseline的頻率增加/減少。 
- 此外當領先/落後進行切換時(產生 polarity)，將會復原回 baseline 的頻率去避免大幅度的震盪。

## U18 EXPERIMENTAL RESULTS (DEMO1) 

<img width="1454" height="371" alt="image" src="https://github.com/user-attachments/assets/cde5ebf2-65f5-4b02-a762-6eed8021efdc" />
<img width="1457" height="408" alt="image" src="https://github.com/user-attachments/assets/254b3c1e-5768-4435-a513-d54302e01535" />
<img width="1453" height="405" alt="image" src="https://github.com/user-attachments/assets/c52d401b-ce44-4784-9520-eeb347697bbd" />
<img width="1455" height="394" alt="image" src="https://github.com/user-attachments/assets/60d247a6-bb0e-4952-98a0-6323780c5126" />
<img width="1453" height="379" alt="image" src="https://github.com/user-attachments/assets/493f0f40-fe00-4c48-a84a-e84aa93d1d52" />
<img width="1455" height="411" alt="image" src="https://github.com/user-attachments/assets/c2cd2aca-769a-4445-abe1-f70f1cc739e9" />
<img width="1455" height="381" alt="image" src="https://github.com/user-attachments/assets/394acf34-9bad-45ca-9106-87d515b0c26c" />

## U18 EXPERIMENTAL RESULTS (DEMO2)

<img width="1452" height="416" alt="image" src="https://github.com/user-attachments/assets/7c4597db-ba3d-4374-ae92-f6f7b63fe56d" />
<img width="1453" height="383" alt="image" src="https://github.com/user-attachments/assets/b2f21f6c-364b-4807-8571-9b242011b611" />
<img width="1450" height="475" alt="image" src="https://github.com/user-attachments/assets/61f8e830-87e1-44cf-a080-148804366cd9" />
<img width="1457" height="477" alt="image" src="https://github.com/user-attachments/assets/3409d30a-5285-4ebb-9366-b26e7553c856" />
<img width="1454" height="408" alt="image" src="https://github.com/user-attachments/assets/dfab53ac-5396-4865-8102-d400654bc99f" />
<img width="1453" height="396" alt="image" src="https://github.com/user-attachments/assets/837335fe-e916-4f74-9fcc-b23815fae3c5" />
<img width="1459" height="381" alt="image" src="https://github.com/user-attachments/assets/ea131b9a-8f40-4e60-ab46-2815dcd82539" />

## ADFP EXPERIMENTAL RESULTS (DEMO1) 

<img width="1453" height="349" alt="image" src="https://github.com/user-attachments/assets/bc7a5e0c-c04e-4fd8-9a4e-1229742a4820" />
<img width="1450" height="394" alt="image" src="https://github.com/user-attachments/assets/bf4978ca-1472-480d-8faa-b1394d4dce1a" />
<img width="1452" height="384" alt="image" src="https://github.com/user-attachments/assets/2f17e834-ff43-42fe-bb4d-1626d4acb034" />
<img width="1453" height="381" alt="image" src="https://github.com/user-attachments/assets/92d8a44e-088b-4aef-a679-adf8b53f09bb" />
<img width="1451" height="374" alt="image" src="https://github.com/user-attachments/assets/a3c3ba63-2084-4034-b2ce-41dd38e7276c" />
<img width="1453" height="408" alt="image" src="https://github.com/user-attachments/assets/38f24635-3ccc-48e3-b3e2-a6d8a9e1c0d6" />
<img width="1455" height="388" alt="image" src="https://github.com/user-attachments/assets/ded69ea0-edc6-44a3-85af-4856fefd5a1c" />

## ADFP EXPERIMENTAL RESULTS (DEMO2)

<img width="1455" height="410" alt="image" src="https://github.com/user-attachments/assets/59e5191f-75e2-47aa-884b-b09d7364e57e" />
<img width="1450" height="402" alt="image" src="https://github.com/user-attachments/assets/7bf82687-93cf-480b-bae0-b177a30a7417" />
<img width="1455" height="402" alt="image" src="https://github.com/user-attachments/assets/ef6f3f17-d2c9-4ee5-9aba-9250ef6d1bce" />
<img width="1453" height="399" alt="image" src="https://github.com/user-attachments/assets/fb9b0ab1-85d9-4627-801a-786402869496" />
<img width="1450" height="376" alt="image" src="https://github.com/user-attachments/assets/03f3f286-bae3-4104-b02d-11239c98fcfb" />
<img width="1456" height="371" alt="image" src="https://github.com/user-attachments/assets/fc1abbd6-544c-4cf7-a32a-3ab8c163846c" />
<img width="1450" height="400" alt="image" src="https://github.com/user-attachments/assets/62bda044-7249-4ea1-9c37-1a60000917de" />

## Specification

<img width="877" height="368" alt="image" src="https://github.com/user-attachments/assets/069baa3a-8183-4f12-8415-0c71a351b38e" />
<img width="877" height="370" alt="image" src="https://github.com/user-attachments/assets/8070b024-df0f-4f79-9dd7-0fe89f64221f" />





