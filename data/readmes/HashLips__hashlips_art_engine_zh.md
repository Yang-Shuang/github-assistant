# 欢迎使用 HashLips 👄

![](https://github.com/HashLips/hashlips_art_engine/blob/main/logo.png)

这些仓库中的所有代码均由 HashLips 在其主 YouTube 频道中创建并讲解。

欲了解更多内容，请访问：

[📺 YouTube](https://www.youtube.com/channel/UC1LV4_VQGBJHTJjEWUmy8nA)

[👄 Discord](https://discord.com/invite/qh6MWhMJDN)

[💬 Telegram](https://t.me/hashlipsnft)

[🐦 Twitter](https://twitter.com/hashlipsnft)

[ℹ️ Website](https://hashlips.online/HashLips)

# HashLips Art Engine 🔥

![](https://github.com/HashLips/hashlips_art_engine/blob/main/banner.png)

使用 Canvas API 和 Node.js 创建生成式艺术。在使用生成引擎之前，请确保已安装 Node.js (v10.18.0)。

## 安装 🛠️

如果你正在克隆该项目，请先运行以下命令；否则你可以从 Release 页面下载源代码并跳过此步骤。

```sh
git clone https://github.com/HashLips/hashlips_art_engine.git
```

若已安装 Yarn，请进入项目根目录并运行以下命令：

```sh
yarn install
```

若已安装 Node.js，也可以运行此命令：

```sh
npm install
```

## 使用指南 ℹ️

在 `layers` 目录中创建不同的图层文件夹，并将所有图层素材添加至这些目录中。你可以自由命名文件，只要文件名中包含稀有度权重（rarity weight）即可，例如：`example element#70.png`。你也可以在 `src/config.js` 文件中将分隔符变量 `rarityDelimiter` 的值从默认的 `#` 更改为你想要的其他字符。

准备好所有图层后，打开 `src/config.js`，将 `layerConfigurations` 对象中的 `layersOrder` 数组更新为你的图层文件夹名称。顺序应从底层（背景）到顶层排列。

_示例：_ 如果你正在制作肖像设计，可能会包含背景、头部、嘴巴、眼睛、眼镜和头饰等图层，那么你的 `layersOrder` 可能如下所示：

```js
const layerConfigurations = [
  {
    growEditionSizeTo: 100,
    layersOrder: [
      { name: "Head" },
      { name: "Mouth" },
      { name: "Eyes" },
      { name: "Eyeswear" },
      { name: "Headwear" },
    ],
  },
];
```

每个图层对象的 `name` 字段代表图片所在的文件夹名称（位于 `/layers/` 目录下）。

你还可以为集合添加多个不同的 `layerConfigurations`。每个配置都可以是独立的，支持不同的图层顺序、复用相同图层或引入新图层。这赋予了创作者在根据需求微调集合时的灵活性。

_示例：_ 如果你正在制作肖像设计，包含背景、头部、嘴巴、眼睛、眼镜和头饰图层，并且想要创建一个新的种族系列，或者只是简单调整图层顺序甚至引入新图层，那么你的 `layerConfigurations` 和 `layersOrder` 可能如下所示：

```js
const layerConfigurations = [
  {
    // Creates up to 50 artworks
    growEditionSizeTo: 50,
    layersOrder: [
      { name: "Background" },
      { name: "Head" },
      { name: "Mouth" },
      { name: "Eyes" },
      { name: "Eyeswear" },
      { name: "Headwear" },
    ],
  },
  {
    // Creates an additional 100 artworks
    growEditionSizeTo: 150,
    layersOrder: [
      { name: "Background" },
      { name: "Head" },
      { name: "Eyes" },
      { name: "Mouth" },
      { name: "Eyeswear" },
      { name: "Headwear" },
      { name: "AlienHeadwear" },
    ],
  },
];
```

更新你的 `format`（输出图片尺寸）大小，以及每个 `layerConfigurations` 对象中的 `growEditionSizeTo` 值，该值表示要生成的变体数量。

若希望打乱图片保存时的 `layerConfigurations` 顺序，可将 `config.js` 文件中的变量 `shuffleLayerConfigurations` 设置为 `true`。默认为 `false`，此时所有图片将按数字顺序保存。

若需要日志进行调试并查看生成图片时的详细情况，可将 `config.js` 文件中的变量 `debugLogs` 设置为 `true`。默认为 `false`，此时仅显示常规日志。

若想尝试不同的混合模式（blending modes），可以在图层顺序的 `options` 对象中添加 `blend: MODE.colorBurn` 字段。

若需要为特定图层设置不同的透明度，同样可以在 `options` 对象中添加 `opacity: 0.7` 字段。

若希望在生成唯一性检查（DNA uniqueness check）时忽略某个图层，可在 `options` 对象中设置 `bypassDNA: true`。例如，这可以确保其余特征保持唯一，而不将 `Background`（背景）图层计入特征组合。该图层仍会包含在最终生成的图片中。

若要使用不同的元数据属性名称（metadata attributes），可在 `options` 对象中添加 `displayName: "Awesome Eye Color"`。所有选项均为可选，且可同时添加在同一图层上。

以下是一个同时使用这些配置字段的示例：

```js
const layerConfigurations = [
  {
    growEditionSizeTo: 5,
    layersOrder: [
      { name: "Background" , {
        options: {
          bypassDNA: false;
        }
      }},
      { name: "Eyeball" },
      {
        name: "Eye color",
        options: {
          blend: MODE.destinationIn,
          opacity: 0.2,
          displayName: "Awesome Eye Color",
        },
      },
      { name: "Iris" },
      { name: "Shine" },
      { name: "Bottom lid", options: { blend: MODE.overlay, opacity: 0.7 } },
      { name: "Top lid" },
    ],
  },
];
```

以下是可选用的不同混合模式列表：

```js
const MODE = {
  sourceOver: "source-over",
  sourceIn: "source-in",
  sourceOut: "source-out",
  sourceAtop: "source-out",
  destinationOver: "destination-over",
  destinationIn: "destination-in",
  destinationOut: "destination-out",
  destinationAtop: "destination-atop",
  lighter: "lighter",
  copy: "copy",
  xor: "xor",
  multiply: "multiply",
  screen: "screen",
  overlay: "overlay",
  darken: "darken",
  lighten: "lighten",
  colorDodge: "color-dodge",
  colorBurn: "color-burn",
  hardLight: "hard-light",
  softLight: "soft-light",
  difference: "difference",
  exclusion: "exclusion",
  hue: "hue",
  saturation: "saturation",
  color: "color",
  luminosity: "luminosity",
};
```

准备就绪后，运行以下命令。生成的图片将保存在 `build/images` 目录中，JSON 文件则保存在 `build/json` 目录：

```sh
npm run build
```

或

```sh
node index.js
```

程序会将所有图片输出至 `build/images` 目录，并将元数据（metadata）文件输出至 `build/json` 目录。每个集合都会在 `build/json` 目录下生成一个 `_metadata.json` 文件，其中包含该集合的所有元数据信息。此外，`build/json` 文件夹还会包含代表每张独立图片的单个 JSON 文件。单张图片的 JSON 文件格式大致如下：

```json
{
  "dna": "d956cdf4e460508b5ff90c21974124f68d6edc34",
  "name": "#1",
  "description": "This is the description of your NFT project",
  "image": "https://hashlips/nft/1.png",
  "edition": 1,
  "date": 1731990799975,
  "attributes": [
    { "trait_type": "Background", "value": "Black" },
    { "trait_type": "Eyeball", "value": "Red" },
    { "trait_type": "Eye color", "value": "Yellow" },
    { "trait_type": "Iris", "value": "Small" },
    { "trait_type": "Shine", "value": "Shapes" },
    { "trait_type": "Bottom lid", "value": "Low" },
    { "trait_type": "Top lid", "value": "Middle" }
  ],
  "compiler": "HashLips Art Engine"
}
```

你也可以通过在 `config.js` 文件的 `extraMetadata` 对象变量中添加自定义的键值对（key: value），为每个元数据文件附加额外信息。

```js
const extraMetadata = {
  creator: "Daniel Eugene Botha",
};
```

如果不需要额外元数据，只需保持对象为空即可。默认情况下该对象即为空。

```js
const extraMetadata = {};
```

至此，配置完成。

## 工具命令

### 更新 IPFS 的 `baseUri` 和描述信息

运行集合生成后，你可能需要更新 `baseUri` 和描述信息。只需运行以下命令即可：

```sh
npm run update_info
```

### 生成预览图

为你的集合创建预览图片拼贴，运行：

```sh
npm run preview
```

### 从集合生成像素化图片

要将图片转换为像素风格，你需要先准备好待转换的图片列表。因此请先运行一次基础生成器。然后只需执行以下命令：

```sh
npm run pixelate
```

所有图片将输出至 `/build/pixel_images` 目录。若想调整像素化比例，可更新 `src/config.js` 文件中 `pixelFormat` 对象的 `ratio` 属性。左侧数值越小，图片的像素化程度越高。

```js
const pixelFormat = {
  ratio: 5 / 128,
};
```

### 从集合生成 GIF 动图

若要基于已创建的图层导出 GIF，只需将 `src/config.js` 文件中 `gif` 对象的 `export` 设置为 `true`。你还可以调整导出 GIF 的 `repeat`（循环次数）、`quality`（质量）和 `delay`（延迟）。设置 `repeat: -1` 表示仅渲染一次，而 `repeat: 0` 将无限循环播放。

```js
const gif = {
  export: true,
  repeat: 0,
  quality: 100,
  delay: 500,
};
```

### 输出稀有度数据（实验性功能）

若要查看集合中各属性的占比情况，运行：

```sh
npm run rarity
```

输出结果大致如下：

```sh
Trait type: Top lid
{
  trait: 'High',
  chance: '30',
  occurrence: '3 in 20 editions (15.00 %)'
}
{
  trait: 'Low',
  chance: '20',
  occurrence: '3 in 20 editions (15.00 %)'
}
{
  trait: 'Middle',
  chance: '50',
  occurrence: '14 in 20 editions (70.00 %)'
}
```

希望你能用这套代码创作出精彩的艺术作品 👄