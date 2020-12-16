# `【调试代码】实时显示loss`

```python3
loss_sum = []
loss_sum.append(loss_ce.item())
# loss_sum.append(loss_s.item())
# loss_sum.append(loss_t.item())
# loss_sum.append(loss_st.item())
loss_sum.append(mse_s.item())
loss_sum.append(mse_t.item())
#保存loss列表
# loss_sum = np.array([[loss_s.item()]])
loss_sum = np.array([loss_sum])
if k == 0:
    loss_list = loss_sum
else:
    loss_list = np.concatenate((loss_list,loss_sum),0)
if k % 500 == 0:
#每500次画一次就行了
    x = [i for i in range(loss_list.shape[0])]
    # plt.clf()
    plt.title('iter ' + str(x[-1]))
    # plt.subplot(211)
    plt.plot(x, loss_list, linewidth=0.5, linestyle="-")
    # plt.pause(0.1)
    plt.show()
```
