<template>
    
   <section>
       


        <section v-for= "near in m_nearByBusinesses" :key='near.name'>
        <section class='businessBar'>
            <img v-bind:src='near.logoPath' class='busLogo'/>
            <section class='text'>
            <article class='businessName'>{{near.name}}</article>
            <!-- 星级
            <starLevel level=near.details.starClass>
            </starLevel>-->
            <!-- 蜂鸟专送 -->
            <!-- <Hummingbird transport = near.details.appointTransport></Hummingbird> -->
            <h5>
            <p><span>￥{{near.details.designationPrice}}起送/配送费约￥{{near.details.transportFee}}</span>
            </p>
            <p><span class='gray'>{{near.details.distance|currencydecimal}}公里 /</span>
            <span class='eleColor'>{{near.details.time}}</span>
            </p>
            </h5>
            </section>
        </section>
        </section>
    </section>

        <!-- <li v-for="cityArr in cities" v-bind:key="cityArr.city">{{cityArr.city}}</li> -->
   
</template>

<script>
    import axios from 'axios'

export default {
    data(){
        return{
            m_nearByBusinesses:[]
        }
    },
    methods:{
        GetNearbyBusinesses:function(){
            axios.get('https://tina-record.github.io/foodApp/v1/businesses/businessesShow')
            .then(response => (this.decideNearbyBusinesses(response)))
            .catch(function(error){alert("网络无法访问")})
        },
        decideNearbyBusinesses:function(response){
            console.log(response.data)
            if(response.data.statu === 200){
                
                //获取当前城市数据
                this.m_nearByBusinesses = response.data.data;
                console.log(this.m_nearByBusinesses)


            }else{
                alert("服务器出错");
            }
        }
    },
    mounted(){
        this.GetNearbyBusinesses();
    },
    filters: { 
    currencydecimal (value) { 
        value = value /1000;
    return value.toFixed(1) 
    }}

}
</script>

<style lang="less">




.businessBar{
    display: flex;
    padding: 0.5rem 0;
   
    border-bottom: 0.01rem solid #ddd;

    .busLogo{
    height:4rem;
    width:4rem;
    flex:1;
    }


    .text{
         flex:9;
        display: flex;
        flex-direction:column;
        justify-content: space-between;
        margin:0 0.5rem;
        .businessName{
            font-weight: 900;
        }

        h5{
            display:flex;
            justify-content: space-between;
            width:100%;
            margin: 0;
            color: #555;
            font-size: 0.65rem;
            p{
            display: inline;
            .eleColor{
            color:hsl(220, 50%, 50%);
            }
            
            
            font-weight: 100;
            .gray{
                color:#777
            }
        }
        }
        

    }

}



</style>
