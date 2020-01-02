<template>
	<Row>
		<Col span="18">
			<card>
				<Table border :columns="columns7" :data="data6"></Table>
			</card>
		</Col>
	</Row>
</template>
<script>
export default {
	data() {
		return {
			columns7: [
				{
					title: 'Name',
					key: 'name',
					render: (h, params) => {
						return h('div', [
							h('Icon', {
								props: {
									type: 'person'
								}
							}),
							h('strong', params.row.name)
						])
					}
				},
				{
					title: 'Age',
					key: 'age'
				},
				{
					title: 'Address',
					key: 'address'
				},
				{
					title: 'Action',
					key: 'action',
					width: 200,
					align: 'center',
					render: (h, params) => {
						return h('div', [
							h(
								'Button',
								{
									props: {
										type: 'primary',
										size: 'small'
									},
									style: {
										marginRight: '5px'
									},
									on: {
										click: () => {
                      console.log(params)
											this.show(params.index)
										}
									}
								}, '详细'),
							h(
								'Button',
								{
									props: {
										type: 'error',
										size: 'small'
                  },
                  style: {
										marginRight: '5px'
									},
									on: {
										click: () => {
											this.remove(params.index)
										}
									}
								}, '删除'),
							h(
								'Button',
								{
									props: {
										type: params.row.type ? 'success' : 'warning',
										size: 'small'
									},
									on: {
										click: () => {
											this.reboot(params.index)
										}
									}
								}, params.row.type ? '正常' : '重启')
						])
					}
				}
			],
			data6: [
				{
          type: 0,
					name: 'niuniu',
					age: 18,
          address: 'New York No. 1 Lake Park'
				},
				{
          type: 1,
					name: 'cancan',
					age: 24,
					address: 'London No. 1 Lake Park'
				},
				{
          type: 0,
					name: 'Joe',
					age: 30,
					address: 'Sydney No. 1 Lake Park'
				},
				{
          type: 1,
					name: 'Joy',
					age: 26,
					address: 'Ottawa No. 2 Lake Park'
				}
			]
		}
	},
	methods: {
		show(index) {
			this.$Modal.info({
				title: 'User Info',
				content: `Name：${this.data6[index].name}<br>Age：${this.data6[index].age}<br>Address：${this.data6[index].address}`
			})
		},
		remove(index) {
			this.data6.splice(index, 1)
    },
    reboot(index) {
      if (this.data6[index].type) {
        this.$Message.error('第' + (index + 1) + '行数据下架');
      } else {
        this.$Message.success('重启了第' + (index + 1) + '行数据');
      }
      this.data6[index].type = !this.data6[index].type
    }
	}
}
</script>
