<script setup>
	import { ref } from 'vue';

	const products = ref([
		{
			id: 1,
			name: "珍珠奶茶",
			description: "香濃奶茶搭配QQ珍珠",
			price: 50,
			stock: 20
		},
		{
			id: 2,
			name: "冬瓜檸檬",
			description: "清新冬瓜配上新鮮檸檬",
			price: 45,
			stock: 18
		},
		{
			id: 3,
			name: "翡翠檸檬",
			description: "綠茶與檸檬的完美結合",
			price: 55,
			stock: 34
		},
		{
			id: 4,
			name: "四季春茶",
			description: "香醇四季春茶，回甘無比",
			price: 45,
			stock: 10
		},
		{
			id: 5,
			name: "阿薩姆奶茶",
			description: "阿薩姆紅茶搭配香醇鮮奶",
			price: 50,
			stock: 25
		},
		{
			id: 6,
			name: "檸檬冰茶",
			description: "檸檬與冰茶的清新組合",
			price: 45,
			stock: 20
		},
		{
			id: 7,
			name: "芒果綠茶",
			description: "芒果與綠茶的獨特風味",
			price: 55,
			stock: 18
		},
		{
			id: 8,
			name: "抹茶拿鐵",
			description: "抹茶與鮮奶的絕配",
			price: 60,
			stock: 20
		}
	]);

	const stockManage = (item, operation) => {
		switch (operation) {
			case 'add':
				item.stock++;
				break;

			case 'sub':
				item.stock--;
				break;

			default:
				console.log('Something went wrong.');
				break;
		}
	}

	const tempEditValue = ref(
		{
			id: '',
			name: ''
		}
	)

	const onEdit = (item) => {
		tempEditValue.value = {...item};
	}

	const onSave = () => {
		const index = products.value.findIndex(item => item.id === tempEditValue.value.id);
		products.value[index].name = tempEditValue.value.name;
		tempEditValue.value = {};
	}
</script>

<template>
	<table>
		<thead>
			<tr>
				<th scope="col">功能</th>
				<th scope="col">品項</th>
				<th scope="col">描述</th>
				<th scope="col">價格</th>
				<th scope="col">庫存</th>
			</tr>
		</thead>
		<tbody>
			<tr v-for="item in products">
				<td>
					<button type="button" v-on:click="onEdit(item)">Edit</button>
				</td>
				<td>{{ item.name }}</td>
				<td><small>{{ item.description }}</small></td>
				<td>{{ item.price }}</td>
				<td><button type="button" v-on:click="stockManage(item, 'sub')">-</button>{{ item.stock }}<button type="button" v-on:click="stockManage(item, 'add')">+</button></td>
			</tr>
		</tbody>
	</table>
	<hr>
	<div v-if="tempEditValue.id">
		<h2>編輯區域</h2>
		<div>
			{{ tempEditValue.name }}
		</div>
		<input type="text" v-model="tempEditValue.name">
		<button type="button" v-on:click="onSave">Save</button>
		<button type="button" v-on:click="tempEditValue = {}">Cancel</button>
	</div>
</template>
