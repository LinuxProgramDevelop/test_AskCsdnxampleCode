<template>
	<div>
	  <div id="mountNode"></div>
	</div>
  </template>
  
  <script>
  import G6 from '@antv/g6';
  
  export default {
	name: 'ProjectMind',
	mounted() {
	  this.initG6()
	},
	data() {
	  return {
		   value: [],
  
	  }
	},
  methods: {
	   initG6() {
		  const data = { "id": "17", "name": "proName", "children": [ { "id": "18", "name": "前期准备阶段", "warning": "true", "layer": "1", "children": [ {"id": "19", "name": "前期调研",href: "dyurl","layer": "2"}, {"id": "20", "name": "指标设计",href: "zburl", "layer": "2"}, {"id": "23", "name": "问卷设计",href: "wjurl", "layer": "2"}, {"id": "24", "name": "方案撰写",href: "faurl", "layer": "2"}, ] }, { "id": "28", "name": "指标评价阶段", "layer": "1", "children": [ {"id": "21", "name": "初步评价阶段"}, {"id": "22", "name": "专家评分"}, {"id": "30", "name": "问卷分析"} ] }, { "id": "29", "name": "结果报告阶段", "children": [ {"id": "31", "name": "指标评分"}, {"id": "32", "name": "报告撰写"}, { "id": "17", "name": "proName", "children": [ { "id": "18", "name": "前期准备阶段", "warning": "true", "layer": "1", "children": [ {"id": "19", "name": "前期调研",href: "dyurl","layer": "2"}, {"id": "20", "name": "指标设计",href: "zburl", "layer": "2"}, {"id": "23", "name": "问卷设计",href: "wjurl", "layer": "2"}, {"id": "24", "name": "方案撰写",href: "faurl", "layer": "2"}, ] }, { "id": "28", "name": "指标评价阶段", "layer": "1", "children": [ {"id": "21", "name": "初步评价阶段"}, {"id": "22", "name": "专家评分"}, {"id": "30", "name": "问卷分析"} ] }, { "id": "29", "name": "结果报告阶段", "children": [ {"id": "31", "name": "指标评分"}, {"id": "32", "name": "报告撰写"}, ] } ] }] } ] };
		  const container = document.getElementById('mountNode');
		  
		  const fadfad="helloworld";
  
  
		  const toolbar = new G6.ToolBar({
			  container: container,
			  getContent: () => {
				  return `
				  <ul>
					  <li code=add'' style="width: 60px">${fadfad}</li>
					  <li code='undo'>撤销</li>
				  </ul>
				  `
			  },
			  handleClick: (code, graph) => {
				  console.log("[DEBUG]: 用户点击了功能框，需要进行搜索等信息");
			  }
		  });
  
			//Menu操作菜单
		  const menu = new G6.Menu({
			  getContent(e) {
				  return (
				  <el-input  placeholder="请输入内容"></el-input>)
				  
			  },
			  handleMenuClick(target, item) {
				  console.log(target, 'target')
				  console.log(item, 'item')
			  }
		  })
  
		  const treeGraph = new G6.TreeGraph({
			  container: 'mountNode',
			  width: document.documentElement.clientWidth,
			  height: document.documentElement.clientHeight,
			  nodeStateStyles: {
				  selected: {
				  fill: 'Cyan',
				  lineWidth: 1,
				  },
				  hover: {
				  fill: 'red',
				  lineWidth: 1,
				  },
			  },
			  plugins:[menu,toolbar],
			  modes: {
				  default: [
				  {
					  type: 'collapse-expand',
				  },
				  //多选节点
				  {
					  type:'brush-select',
					  trigger: 'alt',
					  multiple: true,
				  },
				  'drag-canvas',
				  'drag-node',
				  'scroll-canvas',
				  ],
			  },
			  layout: {
				  type: 'mindmap',
				  direction: 'H',
				  getHeight: () => {
					  return 56;
				  },
				  getWidth: () => {
					  return 16;
				  },
				  getVGap: () => {
					  return 10;
				  },
				  getHGap: () => {
					  return 100;
				  },
				  getSide: () => {
					  return 'right';
				  },
			  },
		  });
  
  
  
		  //对着画布双击触发事件
		  treeGraph.on("canvas:dblclick", evt => {
			  console.log("[DEBUG]: 用户双击了画布，需要增加节点")
		  })
		  treeGraph.data(data);
		  treeGraph.render();
		  treeGraph.fitView();
  
		  if (typeof window !== 'undefined')
		  window.onresize = () => {
			  if (!graph || graph.get('destroyed')) return;
			  if (!container || !container.scrollWidth || !container.scrollHeight) return;
			  graph.changeSize(container.scrollWidth, container.scrollHeight);
		  };
	  }
  }
  }
  
	
  
  </script>