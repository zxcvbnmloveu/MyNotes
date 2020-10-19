# `pytorch中KL散度的计算`

直接用 nn.KLDivLoss()(a,b) 或 F.kl_div(a,b), a,b 是softmax输出时，得到的值是负的。

这里输入的a应为log softmax ，b 是我们的target，不取log计算错误，得到负值。
