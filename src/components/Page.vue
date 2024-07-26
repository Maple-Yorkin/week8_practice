<script setup lang="ts">
import '@/assets/Page.css'
import { onMounted, ref } from 'vue';

  const goodsList = [
      {
        id: '4001172',
        name: '称心如意手摇咖啡磨豆机咖啡豆研磨机',
        price: 289.9,
        picture: 'https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg',
        count: 2,
        spec: { color: '白色' }
      },
      {
        id: '4001009',
        name: '竹制干泡茶盘正方形沥水茶台品茶盘',
        price: 109.8,
        picture: 'https://yanxuan-item.nosdn.127.net/2d942d6bc94f1e230763e1a5a3b379e1.png',
        count: 3,
        spec: { size: '40cm*40cm', color: '黑色' }
      },
      {
        id: '4001874',
        name: '古法温酒汝瓷酒具套装白酒杯莲花温酒器',
        price: 488,
        picture: 'https://yanxuan-item.nosdn.127.net/44e51622800e4fceb6bee8e616da85fd.png',
        count: 1,
        spec: { color: '青色', sum: '一大四小' }
      },
      {
        id: '4001649',
        name: '大师监制龙泉青瓷茶叶罐',
        price: 139,
        picture: 'https://yanxuan-item.nosdn.127.net/4356c9fc150753775fe56b465314f1eb.png',
        count: 1,
        spec: { size: '小号', color: '紫色' },
        gift: '50g茶叶,清洗球'
      }
    ]
  
  //数据渲染：利用map遍历，并用join转换为字符串，交给list大盒子
  const str : string = goodsList.map(item=>{
    const gift = item.gift?item.gift.split(',').map(i=> `<span class="tag">【赠品】${i}</span>`).join(''):''
    const spec = Object.values(item.spec).join('/')
    const price = ((item.price * 100 * item.count) / 100).toFixed(2)
    return `
      <div class="item">
        <img src=${item.picture} alt="">
        <p class="name">${item.name}${gift} </p>
        <p class="spec">${spec}</p>
        <p class="price">${item.price.toFixed(2)}</p>
        <p class="count">x${item.count}</p>
        <p class="sub-total">${price}</p>
      </div>
    `
  }).join('');
  
  const totalPrice = goodsList.reduce((prev, current)=> prev + (current.price * 100 * current.count) / 100, 0)
  const listDiv = ref(null)
  const totalAmount = ref(null)
  onMounted(()=>{
    if(listDiv.value) {
     ( listDiv.value as Element).innerHTML = str
    }
    if(totalAmount.value) {
      (totalAmount.value as Element).innerHTML = totalPrice.toFixed(2)
    }
  })
</script>

<template>
  <div class="list" ref = "listDiv">
    <!-- <div class="item">
      <img src="https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg" alt="">
      <p class="name">称心如意手摇咖啡磨豆机咖啡豆研磨机 <span class="tag">【赠品】10优惠券</span></p>
      <p class="spec">白色/10寸</p>
      <p class="price">289.90</p>
      <p class="count">x2</p>
      <p class="sub-total">579.80</p>
    </div> -->
  </div>
  <div class="total">
    <div>合计：<span class="amount" ref = "totalAmount">1000.00</span></div>
  </div>
</template>

<style scoped>
  
</style>
