# 🎸 🎶 MLOps Lab Exercises (AI500)

## Slide Decks
Slide decks are published alongside the exercise instructions. 

👨‍🏫 👉 [The Published Slides Live Here](https://rhoai-mlops.github.io/lab-instructions/slides/ai500-index.html) 👈 🧑‍💻

## 🪄 Customize The Instructions
The box on the top of the page allows you to render the instructions in this training by replacing those values in the instructions. All you have to do is fill in the boxes on the top of the page with your teams name in the box and the domain your cluster is using and hit `save`. This will persist the values in your local storage for the site - so hitting `clear` will reset these for you if you made a mistake.

* If my team is called `biscuits` then pop that in the first box. This value will be prefixed to some of the things such as the namespaces we use.
* For the cluster domain, you want to add the `apps.*` the bit from the OpenShift domain. For example, if my console address lives at <code class="language-yaml">https://console-openshift-console.apps.hivec.sandbox1243.opentlc.com/</code>
 then just put `apps.hivec.sandbox1243.opentlc.com` in the box to generate the correct address for the exercises.
* For the git server, you could use your preferred and accessible Git server (GitHub, GitLab, ...). The instructor could provide you one.
For example, if the git server lives at <code class="language-yaml">https://gitea.apps.hivec.sandbox1243.opentlc.com/</code>, then just
put `gitea-gitea.apps.hivec.sandbox1243.opentlc.com` in the box to generate the correct address for the exercises.

## 🦆 Conventions
When running through the exercise, we tried to call out where things need replacing. The key ones are anything inside an `<>`, and should be replaced. For example, if your team is called `biscuits` then in the instructions if you see `<USER_NAME>` this should be replaced with `biscuits` like so:
    <div class="highlight" style="background: #f7f7f7">
    <pre><code class="language-bash">
    name: &lt;USER_NAME&gt;
    # ^ this becomes
    name: biscuits
    </code></pre></div>

There are lots of code blocks for you to copy and paste. They have a little ✂️ icon on the right if you move your cursor on the code block. 
```bash
echo "like this one :)"
```
You should not copy and paste the blocks that don't have the copy ✂️ icon. That means you should validate your outputs or yamls against the given block.