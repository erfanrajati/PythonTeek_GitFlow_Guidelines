## **1. Introduction to Git for Unity Game Development**
   - **Why Git in Unity?**
     - Version control is crucial in game development due to large files (e.g., assets, prefabs) and collaborative workflows.
     - Helps avoid conflicts with large binary files through **Git LFS** (Large File Storage).

## **2. Initial Setup**
   - **Step 1: Initialize Unity Project**
     - Make sure `.gitignore` includes all necessary Unity and temporary files like:
       ```
       # Unity specific files
       [Ll]ibrary/
       [Tt]emp/
       [Oo]bj/
       [Bb]uild/
       ```
   - **Step 2: Initialize Git Repository**
     - In the Unity project directory, run:
       ```bash
       git init
       git add .
       git commit -m "Initial commit"
       ```

   - **Step 3: Create Remote Repository on GitHub/GitLab**
     - Create a GitHub or GitLab repository for your Unity project.

   - **Step 4: Link Local Repo to Remote**
     - Use the following command:
       ```bash
       git remote add origin <URL>
       git push -u origin main
       ```

## **3. Git Branching Strategy**
   Your branch structure is clear, but we can expand it:

   - **Main Branch (`main`)**: 
     - This is the most stable version of the game, with tags corresponding to release versions (e.g., `v1.0.0`).
   
   - **Develop Branch (`develop`)**:
     - Used as the main integration branch where features are merged after development.

   - **Feature Branches (`feature/<task-name>`)**:
     - These branches are where specific features or tasks are developed. Each feature/task gets its branch.
     - Naming Convention: `feature/jump-animation` or `feature/new-enemy-AI`.

   - **Research Branches (`research/<package-name>`)**:
     - These branches are for testing or experimenting with new Unity packages (e.g., physics engines, visual effects libraries).
     - These branches aren't merged back into `develop` after the research is finished.
     - If the research was successful, a `feature` branch is made from `develop` and the development begins.

   - **Hotfix Branches (`hotfix/<issue-name>`)**:
     - Used to fix urgent bugs on the main production release.

## **4. Commit Strategy**
   Your team should follow structured commits to keep the history clean and meaningful.

   - **1 Commit per Subtask**:
     - After completing a specific task or milestone, commit changes with descriptive messages.

   - **Commit Message Guidelines**:
     - **Structure**: Use [Conventional Commits](https://www.conventionalcommits.org/) for clarity:
       ```
        <type>[optional scope]: <description>

        [optional body]
        
        [optional footer(s)]
       ```
     - **Types**:
       - `feat`: Adding assets or completing a feature milestone.  
       - `fix`: Fixing a bug or glitch.
       - `docs`: Documentation changes.
       - `style`: Code style changes (e.g., formatting).
       - `refactor`: Code restructuring.
       - `test`: Adding or updating tests.

     **Examples**:
     - `feat(jump): Add new jump animation`
     - `feat(assets): add new environment textures and models`
     - `fix(camera): Fix the camera controller in level 2`
     - `feat(assets): add forest textures and tree models`
     - `feat(assets): add background music and sound effects for level 1`
     - `feat(assets): add new character sprites and animations`

## **5. Pull Requests (PRs) and Code Reviews**
   - **Creating PRs**:
     - Ensure that each feature or task has its corresponding PR.
     - Include a description of what the feature/bug fix does, screenshots of the feature (if applicable), and any additional testing steps.
   
   - **Review Process**:
     - At least one code review should be done by a senior developer.
     - Ensure code adheres to Unity coding conventions, and avoid pushing unnecessary changes (like Unity-generated files).

## **6. Handling Large Files and Git LFS**
   - **Using Git LFS**:
     - For Unity projects, large binary files (textures, models, sounds) should be handled using Git LFS to avoid large repository sizes and long load times:
       ```bash
       git lfs track "*.psd"
       git lfs track "*.fbx"
       git add .gitattributes
       ```
   - **More details about Git LFS at section 

## **7. Tagging and Versioning**
   - **Semantic Versioning**:
     - Follow [Semantic Versioning](https://semver.org/) for releases, tagging them as:
       - `v1.0.0` for major releases.
       - `v1.0.1` for patch/hotfix releases.
   
   - **Creating a Tag**:
     ```bash
     git tag -a v1.0.0 -m "Release version 1.0.0"
     git push origin v1.0.0
     ```

## **8. Best Practices for Unity and Git**
   - **Frequent Commits**: Make small, frequent commits with meaningful messages.
   - **Avoid Committing Unity-Specific Files**: Use the `.gitignore` to avoid adding unnecessary Unity files (e.g., `Library/` and `Temp/` folders).
   - **Test Before Merging**: Always test branches in Unity before merging them into `develop` or `main`.
   - **Conflict Resolution**: Resolve merge conflicts by testing the game in Unity after the merge to ensure nothing broke due to asset merges.



## **9. Handling Large Files and Git LFS**

In Unity projects, you often work with large binary files, such as textures, models, audio files, and video clips. These files can quickly bloat your repository, making it slow to clone and difficult to manage. This is where **Git LFS (Large File Storage)** comes in.

### **What is Git LFS?**
Git LFS is an extension for Git that helps you manage large files more efficiently. Instead of storing the actual large file content in your Git repository, Git LFS stores a small reference file in Git, while the actual large files are kept separately. This keeps your repository lightweight and speeds up operations like cloning and pulling changes.

When you clone or pull a repository with Git LFS, it automatically downloads the large files referenced in the repository.

### **Why Use Git LFS for Unity Projects?**
Unity projects tend to have large assets, such as:
- Textures and Sprites (e.g., `.png`, `.jpg`, `.psd`)
- 3D Models (e.g., `.fbx`, `.obj`)
- Audio (e.g., `.wav`, `.mp3`)
- Video (e.g., `.mp4`)

Without Git LFS, committing these large files directly into Git makes the repository slow to download and can lead to poor performance during collaboration. Git LFS allows your team to handle these large assets in a way that doesn’t slow down version control operations.

### **How to Set Up Git LFS**

1. **Install Git LFS** (if not installed):
   - Follow the instructions on [Git LFS official site](https://git-lfs.github.com/) to install it.
   - After installation, run this command to enable Git LFS in your project:
     ```bash
     git lfs install
     ```

2. **Track Large Files**:
   You need to specify which file types Git LFS should manage in your Unity project. For example, to track common large file types like textures, models, and audio, you would run the following commands:
   ```bash
   git lfs track "*.psd"  # Track Photoshop files
   git lfs track "*.fbx"  # Track 3D model files
   git lfs track "*.wav"  # Track audio files
   git lfs track "*.mp4"  # Track video files
   ```
   This creates a `.gitattributes` file in your project that tells Git which files to manage with LFS.

3. **Commit the Changes**:
   Once you've added files to Git LFS, commit the changes, including the `.gitattributes` file:
   ```bash
   git add .gitattributes
   git add .
   git commit -m "Track large files with Git LFS"
   ```

4. **Push to Remote Repository**:
   Push your changes to your Git remote (e.g., GitHub or GitLab). Git LFS will handle uploading the large files to a separate storage area:
   ```bash
   git push origin main
   ```

### **How Git LFS Works**
When you use Git LFS, the large files (such as textures or models) are not stored in Git’s history. Instead, a small pointer file is saved in Git, while the actual content is stored on a separate server. This reduces the repository size and speeds up operations like `clone` and `fetch`.

- When another developer pulls the repository, Git LFS will automatically download the latest versions of the large files.
- When you push changes, Git LFS pushes the large files separately from the rest of the repository content.

### **Best Practices for Using Git LFS**
- **Track only large files**: Avoid tracking small text files (like scripts or configuration files) with Git LFS, as this would add unnecessary complexity.
- **Keep an eye on storage limits**: Some platforms like GitHub or GitLab have storage quotas for Git LFS, so monitor your usage.
