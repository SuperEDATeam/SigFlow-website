<script>
// 按顺序导入9个头像文件（与给定的文件名和顺序严格对应）
import avatar1 from '@/assets/images/headimg/headimg1.jpg'
import avatar2 from '@/assets/images/headimg/headimg2.jpg'
import avatar3 from '@/assets/images/headimg/headimg3.jpg'
import avatar4 from '@/assets/images/headimg/headimg4.jpg'
import avatar5 from '@/assets/images/headimg/headimg5.png'
import avatar6 from '@/assets/images/headimg/headimg6.jpg'
import avatar7 from '@/assets/images/headimg/headimg7.jpg'
import avatar8 from '@/assets/images/headimg/headimg8.jpg'
import avatar9 from '@/assets/images/headimg/headimg9.png'

export default {
  name: 'TeamComments',
  data() {
    return {
      // 评论内容数组（共9人，索引0和5为有效评论，其余为空字符串）
      comments: [
        '“SigFlow是一次具有开拓意义的探索，表面上看，它打破了Verilog和电路图的不等价壁垒，实质上，其抓住了逻辑电路建模的统一抽象层次。”',
        '“SigFlow能将Verilog代码映射为逻辑门电路，助初学者理解硬件描述语言与底层电路。AI助手据需求自动生成Verilog代码及对应电路，实现需求到电路可视化，让学习更平缓，入门更便捷高效。”',
        '“做芯片工程师这件事，确实正变得越来越有趣。我们目前只触及了可能性的1%，而像SigFlow这样的交互式体验，正是AI+EDA这类软件最能大放异彩的地方。”',
        '“我们的目标与贵方设计系统高度契合，拟构建基于中间数据结构的Verilog与电路图双向同步设计平台，开发中提供实时高效的视觉反馈，直观呈现电路信号逻辑，并深度集成EDA工具链上下游。相信贵团队的专业经验与资源，将为项目落地提供有力技术支撑与保障。”',
        '“我公司技术团队测试后认为，SigFlow软件的设计理念与我们高度一致。该平台实现Verilog与电路图双向同步，开发中提供实时视觉反馈，清晰展示信号流动逻辑，并深度集成EDA工具链。我们高度认可其商业价值，相信贵团队的专业经验与资源能有效支撑项目成功落地。”',
        '“这是一款优秀的硬件设计平台，其 AI 插件堪称点睛之笔，彻底改变了我对‘AI 辅助 EDA 设计’的认知。整个插件界面简洁有力，左侧的会话管理功能让不同模块的设计进度一目了然。它内置了很多实用的命令，极大提升了设计效率。”',
        '“工具的价值在于赋予用户表达的自由。当工程师能用熟悉的符号绘制电路，而非被强制使用标准图库时，技术便从束缚变为延伸。平衡图案灵活性与代码准确性的过程，也让我重新理解了‘好的工程工具应当是隐形的’——让用户专注设计，而非适应工具。”',
        '“SigFlow让我重新理解了“设计”与“实现”的边界。过去做硬件开发，常需在逻辑架构与底层门电路间反复权衡，思路易被实现细节打断。如今借助其逻辑黑箱与AI协同，我可先专注顶层架构，底层交由AI完成；需极致优化时，也能深入底层手动调优。这种双向赋能模式，真正实现“想得快、落得稳。”',
        '“SigFlow 重新定义了硬件设计的工作流体验：它不仅是电路编辑的载体，更是从EDA设计，到硬件语言融合，再到波形读取等硬件设计的全流程融合尝试，再结合逻辑黑箱与 AI 辅助设计的能力，让设计者既能摆脱底层门电路的繁琐，又能高效追溯项目迭代轨迹。”',
      ],
      // 姓名数组（共9人）
      names: [
        '吾臣悟了~',
        '涛子',
        '湖上有帆',
        '吴啸',
        '宋艳欣',
        '梨花诗',
        'Solo-Eternity',
        '目民',
        '小王',
      ],
      // 职称/身份数组（共9人）
      degrees: [
        'the leader of superEDA, sophomore at UESTC',
        'junior at UESTC, major in industrial software',
        'sophomore at UESTC, circuit design enthusiasts',
        '无锡市久易通科技有限公司技术负责人',
        '北京一三六九网络科技公司联系人',
        'sophomore at UESTC, AI enthusiasts',
        'expert in chip design',
        'IC designer',
        'FPGA lover',
      ],
      // 头像文件数组（顺序与上述数据一致）
      avatars: [avatar1, avatar2, avatar3, avatar4, avatar5, avatar6, avatar7, avatar8, avatar9],
    }
  },
}
</script>

<template>
  <div class="sigflow">
    <div class="text">构建软件的全新方式。</div>
    <ul class="comments">
      <!-- 使用 v-for 动态渲染所有 li，grid 自动排列为每行三个 -->
      <li v-for="(name, index) in names" :key="index">
        <!-- 评论内容框 -->
        <div class="comment">{{ comments[index] }}</div>
        <div class="info">
          <!-- 头像：绑定对应的图片路径，并设置 alt 属性为姓名 -->
          <img :src="avatars[index]" :alt="name" />
          <!-- 姓名 -->
          <div class="name">{{ name }}</div>
          <!-- 职称/身份 -->
          <div class="degree">{{ degrees[index] }}</div>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style: none;
}

.sigflow {
  z-index: 2;
  margin: 0 auto;
  margin-top: 35px;
  padding: 0;
  width: 1200px;
  height: 900px;
}

.sigflow .text {
  z-index: 2;
  margin: 0 auto;
  width: 600px;
  height: 100px;
  text-align: center;
  line-height: 100px;
  font-size: 35px;
  color: white;
}

/* grid 布局：三列，自动按行填充 */
.sigflow .comments {
  z-index: 2;
  display: grid;
  grid-template-columns: 380px 380px 380px;
  gap: 10px 30px;
  width: 1200px;
  height: 770px;
}

/* 基础 li 样式：保留原有宽高和边框 */
.sigflow .comments li {
  z-index: 2;
  width: 380px;
  height: 250px;
  background-color: rgba(230, 243, 255, 0.7);
  border: 1px rgb(214, 234, 252) solid;
}

/* 移除所有手动网格定位，让 li 自动按顺序排列 */
/* 原 nth-child 定位规则已删除，确保三行三列正常显示 */

.sigflow .comments li .comment {
  z-index: 2;
  width: 370px;
  height: 170px;
  margin: 3px;
  /* border: 1px rgb(214, 234, 252) solid; */
  font-size: 17px;
  font-family: 'STZhongsong';
}

.sigflow .comments li .info {
  z-index: 2;
  position: relative;
  width: 370px;
  height: 70px;
  margin: 3px;
  /* border: 1px rgb(214, 234, 252) solid; */
}

.sigflow .comments li .info img {
  z-index: 2;
  position: absolute;
  width: 60px;
  height: 60px;
  top: 2px;
  left: 5px;
  /* border: 1px rgb(214, 234, 252) solid; */
}

.sigflow .comments li .info .name {
  z-index: 2;
  position: absolute;
  top: 5px;
  right: 5px;
  width: 290px;
  height: 25px;
  /* border: 1px rgb(214, 234, 252) solid; */
}

.sigflow .comments li .info .degree {
  z-index: 2;
  position: absolute;
  bottom: 5px;
  right: 5px;
  width: 290px;
  height: 25px;
  font-size: 13px;
  color: rgb(57, 55, 55);
  /* border: 1px rgb(214, 234, 252) solid; */
}
</style>
