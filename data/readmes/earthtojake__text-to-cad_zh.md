<div align="center">

<img src="assets/text-to-cad-demo.gif" alt="Demo of the CAD skill generating and previewing CAD geometry" width="100%">

<br>

<pre>
 ██████╗ █████╗ ██████╗       ███████╗██╗  ██╗██╗██╗     ██╗     ███████╗
██╔════╝██╔══██╗██╔══██╗      ██╔════╝██║ ██╔╝██║██║     ██║     ██╔════╝
██║     ███████║██║  ██║      ███████╗█████╔╝ ██║██║     ██║     ███████╗
██║     ██╔══██║██║  ██║      ╚════██║██╔═██╗ ██║██║     ██║     ╚════██║
╚██████╗██║  ██║██████╔╝      ███████║██║  ██╗██║███████╗███████╗███████║
 ╚═════╝╚═╝  ╚═╝╚═════╝       ╚══════╝╚═╝  ╚═╝╚═╝╚══════╝╚══════╝╚══════╝
</pre>

面向计算机辅助设计（CAD）、机器人及硬件设计智能体的技能库

[Docs](https://www.cadskills.xyz) | [Demo](https://demo.cadskills.xyz)

[![GitHub stars](https://img.shields.io/github/stars/earthtojake/text-to-cad?style=for-the-badge&logo=github&label=Stars)](https://github.com/earthtojake/text-to-cad/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/earthtojake/text-to-cad?style=for-the-badge&logo=github&label=Forks)](https://github.com/earthtojake/text-to-cad/network/members)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![Follow @earthtojake](https://img.shields.io/badge/Follow-%40earthtojake-000000?style=for-the-badge&logo=x)](https://x.com/earthtojake)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)](skills/cad/requirements.txt)
[![build123d](https://img.shields.io/badge/build123d-CAD-00A676?style=for-the-badge)](https://github.com/gumyr/build123d)
[![OCP](https://img.shields.io/badge/OCP-OpenCascade-2F80ED?style=for-the-badge)](skills/cad/requirements.txt)
[![STEP](https://img.shields.io/badge/STEP-Export-4A5568?style=for-the-badge)](skills/cad/SKILL.md)
[![STL](https://img.shields.io/badge/STL-Export-4A5568?style=for-the-badge)](skills/cad/SKILL.md)
[![3MF](https://img.shields.io/badge/3MF-Export-4A5568?style=for-the-badge)](skills/cad/SKILL.md)
[![URDF](https://img.shields.io/badge/URDF-Robots-6B46C1?style=for-the-badge)](skills/urdf/SKILL.md)
[![SDF](https://img.shields.io/badge/SDF-Simulation-6B46C1?style=for-the-badge)](skills/sdf/SKILL.md)
[![SRDF](https://img.shields.io/badge/SRDF-MoveIt2-6B46C1?style=for-the-badge)](skills/srdf/SKILL.md)

</div>

# CAD 技能库

CAD Skills 是一个面向计算机辅助设计（CAD）、机器人及硬件设计智能体的技能库，用于从本地项目文件中生成、检查、获取、切片以及移交相关工件。

## 🧰 技能列表

安装该库可为智能体提供针对 CAD 设计、制造、机器人描述文件、仿真及本地审查的专注工作流。

<table>
  <tr>
    <th>Skill</th>
    <th>Summary</th>
    <th>Source</th>
  </tr>
  <tr>
    <td>CAD</td>
    <td>根据自然语言或图片请求创建和编辑 CAD 模型，主要输出 STEP 格式，并支持导出为 STL、3MF 和 GLB。</td>
    <td><a href="skills/cad/SKILL.md"><strong>skills/cad</strong></a></td>
  </tr>
  <tr>
    <td>CAD Viewer</td>
    <td>在本地浏览器中预览 CAD、G-code（G代码）及机器人文件。</td>
    <td><a href="skills/cad-viewer/SKILL.md"><strong>skills/cad-viewer</strong></a></td>
  </tr>
  <tr>
    <td>step.parts</td>
    <td>查找现成的标准 STEP 零件，如螺丝、轴承、电机和连接器等。</td>
    <td><a href="skills/step-parts/SKILL.md"><strong>skills/step-parts</strong></a></td>
  </tr>
  <tr>
    <td>URDF</td>
    <td>编写包含连杆、关节、限位、惯性参数及网格的机器人结构文件。</td>
    <td><a href="skills/urdf/SKILL.md"><strong>skills/urdf</strong></a></td>
  </tr>
  <tr>
    <td>SRDF</td>
    <td>为 URDF 添加 MoveIt 规划组、末端执行器、位姿及碰撞规则。</td>
    <td><a href="skills/srdf/SKILL.md"><strong>skills/srdf</strong></a></td>
  </tr>
  <tr>
    <td>SDF</td>
    <td>创建包含框架、物理属性、传感器和灯光的仿真模型与世界。</td>
    <td><a href="skills/sdf/SKILL.md"><strong>skills/sdf</strong></a></td>
  </tr>
  <tr>
    <td>SendCutSend</td>
    <td>在上传至 SendCutSend 前检查 DXF 与 STEP 文件。</td>
    <td><a href="skills/sendcutsend/SKILL.md"><strong>skills/sendcutsend</strong></a></td>
  </tr>
  <tr>
    <td>G-code</td>
    <td>使用真实的切片器 CLI，将支持的网格文件切片为经过验证且符合打印机配置文件的 FDM `.gcode`。</td>
    <td><a href="skills/gcode/SKILL.md"><strong>skills/gcode</strong></a></td>
  </tr>
  <tr>
    <td>Bambu Labs</td>
    <td>基于已验证的 `.gcode` 文件进行本地 Bambu Lab 打印任务的模拟运行、上传及谨慎启动。</td>
    <td><a href="skills/bambu-labs/SKILL.md"><strong>skills/bambu-labs</strong></a></td>
  </tr>
</table>

## 💻 安装指南

生产环境使用时，请从 `main` 分支安装或克隆；该分支包含供应商安装程序所需的生成型技能/插件输出。

### 技能（Skills）

使用 Skills CLI 安装 CAD Skills：

```bash
npx skills install earthtojake/text-to-cad
```

这是推荐的安装方式。它会将各个技能直接安装到受支持的智能体中。

### 插件（Plugins）

同时也支持通过供应商原生插件方式在 Codex 和 Claude Code 中安装：

```bash
# Codex
codex plugin marketplace add earthtojake/text-to-cad
codex plugin add cad@text-to-cad
```

```bash
# Claude Code
claude plugin marketplace add earthtojake/text-to-cad
claude plugin install cad@text-to-cad
```

如果新安装的技能未显示，请重启智能体。进行本地开发时，请基于 `develop` 分支创建新分支，向 `develop` 提交 PR，并参考 [CONTRIBUTING.md](CONTRIBUTING.md) 中的符号链接工作流。

## 📸 截图演示

<table>
  <tr>
    <td width="33%">
      <a href="./assets/text-to-cad-demo.gif">
        <img src="./assets/text-to-cad-demo.gif" alt="CAD 技能演示：在 CAD Viewer 中显示生成的几何体" width="100%">
      </a>
      <a href="./skills/cad/SKILL.md"><strong>CAD</strong></a>
    </td>
    <td width="33%">
      <a href="./assets/urdf-demo.gif">
        <img src="./assets/urdf-demo.gif" alt="URDF 技能演示：在 CAD Viewer 中显示机器人描述输出" width="100%">
      </a>
      <a href="./skills/urdf/SKILL.md"><strong>URDF</strong></a>
    </td>
    <td width="33%">
      <a href="./assets/srdf-moveit2-demo.gif">
        <img src="./assets/srdf-moveit2-demo.gif" alt="SRDF MoveIt2 技能演示：在 CAD Viewer 中显示逆运动学求解" width="100%">
      </a>
      <a href="./skills/srdf/SKILL.md"><strong>SRDF / MoveIt2</strong></a>
    </td>
  </tr>
</table>

## 🧪 基准测试

该仓库通过 Git LFS 将大型资源文件存储在 `assets/**` 和 `benchmarks/**` 目录中，并在默认 LFS 拉取时排除这些目录树，以便轻量级克隆不会下载 GIF 等资源。基准测试的 Markdown 文件保持为普通 Git 对象以方便查看差异。若只需在本地加载基准测试资源，请运行：

```bash
git lfs pull --include="benchmarks/**"
```

<table>
  <thead>
    <tr>
      <th>#</th>
      <th>Target</th>
      <th>Prompt</th>
      <th>Output</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td><a href="benchmarks/01-rectangular-calibration-block.md">带四个孔的矩形校准块</a></td>
      <td>Create a centered 100 x 60 x 20 mm block with four 8 mm vertical through-holes. Add only a 2 mm chamfer on the top outer perimeter.</td>
      <td><img src="benchmarks/benchmark_01_rectangular_calibration_block.gif" alt="Rectangular calibration block orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>2</td>
      <td><a href="benchmarks/02-circular-flange.md">带螺栓孔图案的圆形法兰</a></td>
      <td>Create an 80 mm diameter, 10 mm thick circular flange with a 30 mm central through-bore. Add six 6 mm through-holes on a 60 mm bolt circle and fillet the outside circular edges.</td>
      <td><img src="benchmarks/benchmark_02_circular_flange.gif" alt="Circular flange orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>3</td>
      <td><a href="benchmarks/03-l-bracket.md">带加强筋和两种方向孔的 L 型支架</a></td>
      <td>Create an L-bracket from a base plate and rear vertical plate. Add vertical base holes, horizontal back-plate holes, two triangular gussets, and a filleted base/back transition.</td>
      <td><img src="benchmarks/benchmark_03_l_bracket.gif" alt="L-bracket orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>4</td>
      <td><a href="benchmarks/04-stepped-shaft-keyway.md">带键槽的阶梯轴</a></td>
      <td>Create a 120 mm shaft along X with 20/30/20 mm diameter stepped sections. Add end chamfers and a shallow rectangular keyway on top of the middle section.</td>
      <td><img src="benchmarks/benchmark_04_stepped_shaft_keyway.gif" alt="Stepped shaft orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>5</td>
      <td><a href="benchmarks/05-open-top-electronics-enclosure.md">带安装柱的开顶电子外壳</a></td>
      <td>Create a hollow open-top enclosure with 3 mm walls and floor. Add four internal standoffs with centered blind holes and 2 mm outside vertical corner fillets.</td>
      <td><img src="benchmarks/benchmark_05_open_top_electronics_enclosure.gif" alt="Open-top electronics enclosure orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>6</td>
      <td><a href="benchmarks/06-clevis-bracket-lightening-cutouts.md">航空级耳型支架带减重孔</a></td>
      <td>Create a symmetric clevis bracket with a base plate, two rounded lugs, base mounting holes, and a horizontal lug bore. Add triangular lightening cutouts, reinforcing ribs, and rounded transitions.</td>
      <td><img src="benchmarks/benchmark_06_clevis_bracket_lightening_cutouts.gif" alt="Clevis bracket orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>7</td>
      <td><a href="benchmarks/07-radial-engine-cylinder.md">带散热翅片的径向发动机缸体</a></td>
      <td>Create a vertical engine-cylinder form with a central barrel, 12 cooling fins, a base flange, and a top cap. Add a 35 degree angled spark-plug boss with a coaxial through-hole.</td>
      <td><img src="benchmarks/benchmark_07_radial_engine_cylinder.gif" alt="Radial-engine-style cylinder orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>8</td>
      <td><a href="benchmarks/08-centrifugal-impeller.md">带后弯叶片的离心叶轮</a></td>
      <td>Create a centrifugal impeller with a backplate, hub, and through-bore. Add 12 fused backward-curved blades sweeping about 45 degrees from root to tip.</td>
      <td><img src="benchmarks/benchmark_08_centrifugal_impeller.gif" alt="Centrifugal impeller orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>9</td>
      <td><a href="benchmarks/09-spiral-staircase.md">带螺旋扶手的旋转楼梯</a></td>
      <td>Create a miniature spiral staircase with a central column, base disk, and 20 rising wedge treads. Add a one-revolution helical handrail and vertical balusters at the tread outer ends.</td>
      <td><img src="benchmarks/benchmark_09_spiral_staircase.gif" alt="Spiral staircase orbit gif" width="220"></td>
    </tr>
    <tr>
      <td>10</td>
      <td><a href="benchmarks/10-planetary-gear-stage.md">简化版行星齿轮机构</a></td>
      <td>Create a flat planetary gear assembly with separate sun, planet, ring, carrier, and pin bodies. Use simplified trapezoidal teeth and place three planets around the sun on a 42 mm radius circle.</td>
      <td><img src="benchmarks/benchmark_10_planetary_gear_stage.gif" alt="Planetary gear stage orbit gif" width="220"></td>
    </tr>
  </tbody>
</table>

## 🛠️ 贡献指南

开发基于 `develop` 分支进行；请向 `develop` 提交 PR，而非 `main`。有关本地贡献工作流、技能链接及验证指南，请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。